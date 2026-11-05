---
name: drone-fly-mobile
description: Verfeinert eine mit `drone-fly` gebaute Fly-through-Website für Smartphones – im selben Projekt und derselben Codebasis. Feste Mobile-Navigation mit Glass-to-Solid-Header, Center-Crop des vorhandenen Desktop-Footage (standardmäßig keine neue Videogenerierung, keine Credits; Hochformat-Stufen nur auf ausdrücklichen Wunsch), Geräteklassen-Auslieferung mit Data-Saver-Fallback, eigenes Mobile-Scroll-Pacing, einspaltige Layouts und Validierung auf mehreren Handygrößen. Verwenden bei "/drone-fly-mobile", "Mobile Refinement", "Drohnen-Website fürs Handy optimieren", "Fly-through mobil anpassen". Setzt eine bestehende drone-fly-Website voraus.
---

# Drone Fly Mobile – Mobile Refinement

Mobile ist ein bewusst komponiertes Erlebnis innerhalb **derselben Website und Codebasis** – keine zweite Seite. Navigation, Typografie, Abstände, Framing des Flugs und Scroll-Timing werden für kleine Screens angepasst. **Das Desktop-Footage wird wiederverwendet; kein neues Video für Mobile generieren** – außer der Nutzer wählt ausdrücklich eine der kostenpflichtigen Hochformat-Stufen (Abschnitt 4a).

Vorher: Projekt, Content-Datei (Beat-Timeline), Manifest und Frame-Sequenz aus `drone-fly` lesen. Nichts Bestehendes überschreiben, ohne es gelesen zu haben.

## 1. Feste Mobile-Navigation

- Kompakte Navigationsleiste oben fixiert – über die ganze Seite, auch nach dem Flug.
- Links Markensymbol + Wortmarke, rechts Hamburger. Beides bleibt beim Scrollen sichtbar. Wortmarke einzeilig: kürzen oder skalieren statt umbrechen.
- Navigation **außerhalb** der gepinnten Fly-through-Sektion mounten, damit sie am Sektionsende nicht verschwindet. `z-index` über Animation und Content.
- Safe-Area-Insets beachten (`env(safe-area-inset-*)`), Touch-Ziele mindestens 44 × 44 px.
- Hamburger öffnet ein barrierefreies Menü: klare Links, Primär-CTA, Schließen-Button, Tastaturbedienung, Fokus-Management (Fokus rein, Fokus-Falle, Fokus zurück), Escape schließt. Nach Link-Auswahl schließen. Hintergrund-Scroll sperren, solange offen.
- Anker-Ziele versetzen, damit der fixe Header keine Überschriften verdeckt: `scroll-padding-top` = Header-Höhe + kleiner Abstand.

## 2. Glass-to-Solid-Header (Mobile und Desktop)

**Über dem Flug (Glass):** durchsichtig, Footage läuft dahinter. Verlauf in der dunkelsten Markenfarbe, oben am stärksten (~70 % Deckkraft), nach unten auf 0 auslaufend – keine harte Kante. Logo, Menü-Icon und CTA müssen auch über den **hellsten** Frames lesbar bleiben – gegen die hellsten Szenen testen, nicht nur gegen den Eröffnungsframe.

**Nach dem Flug (Solid):** fast deckend in derselben Farbe (~90–95 %), `backdrop-filter: blur(10px)` plus `-webkit-backdrop-filter`, feine Hairline-Border. Navigation bleibt über hellen Sektionen, Cards und Formularen scharf.

Umsetzung:

- Zustand aus der Position der Fly-through-Sektion ableiten: Solid, sobald deren Unterkante die Unterkante des Headers erreicht. Neu berechnen bei Scroll (passiver Listener), Resize, Orientierungswechsel und einmal beim Laden (für Aufrufe mitten auf der Seite oder per Anker).
- Nur **eine** Zustandsklasse togglen. Nur Hintergrund, Border und Blur über ~250–350 ms animieren – nie Layout, Höhe oder Position.
- Beim Zurückscrollen in den Flug wieder Glass.
- Offenes Mobile-Menü nutzt immer Solid, egal wo gescrollt.
- `prefers-reduced-motion`: Zustände ohne Transition wechseln.
- Ohne `backdrop-filter`-Support funktioniert Solid trotzdem, weil der Hintergrund fast deckend ist.

## 3. Mobile-Hero-Komposition

Der Flug hat Vorrang. Eröffnungsscreen schlicht:

- fixe Glass-Navigation
- eine kurze Headline
- ein Primär-CTA
- ein dezenter Scroll-Hinweis

Stützende Absätze, dekorative Labels und Sekundär-CTAs entfernen oder kürzen, wenn sie mit dem Footage konkurrieren.

Kapiteltexte auf dem Handy **unten** verankern, über einem weichen Scrim von unten nach oben – nicht neben dem Motiv wie auf Desktop. Frei halten: die Tür/den Weg, auf den die Kamera zufliegt, und die fixe Navigation.

Während des Flugs füllt das Footage den Screen mit minimalen Overlays: pro Kapitel eine kurze Headline, Fließtext gekürzt oder ausgeblendet. Beim Schluss-Luftbild wieder knappe Copy und einen CTA einführen.

## 4. Breitbild-Flug auf Mobile wiederverwenden

Nicht neu animieren. Ein First-Person-Flug hält sein Motiv (Tür, Gang, Weg nach vorn) nahe der horizontalen Bildmitte – daher liest sich dasselbe Footage im Hochformat natürlich, wenn es mittig gecroppt wird.

Canvas bildschirmfüllend mit **Cover-Fit** rendern (Canvas-Äquivalent zu `object-fit: cover`):

```text
scale = max(canvasWidth / frameWidth, canvasHeight / frameHeight)
drawWidth = frameWidth * scale, drawHeight = frameHeight * scale
x = (canvasWidth - drawWidth) / 2, y = (canvasHeight - drawHeight) / 2
```

Backing Store des Canvas = Viewport × devicePixelRatio (gedeckelt auf 2), neu berechnen bei Resize und Orientierungswechsel.

**Crop prüfen, bevor du dich darauf verlässt.** Ein 9:16-Handy zeigt aus 16:9-Footage die mittleren ~45 %. Durch den ganzen Flug kontrollieren, z. B. mit einem gecroppten Kontaktabzug:

```sh
ffmpeg -i flythrough-master.mp4 -vf "fps=1,crop=ih*9/16:ih,scale=-1:360,tile=10x3" -frames:v 1 crop-check.jpg
```

- Türen, Kurven und der Weg nach vorn bleiben im Crop.
- Menschen und Schlüsselobjekte (Mitarbeiter an der Tür, Techniker, Hero-Produkt) werden im entscheidenden Moment nicht halbiert.
- 180°-Drehung und Schluss-Luftbild lesen sich noch; das ganze Gebäude ist im Center-Crop der letzten Frames erkennbar.

Liegt ein Moment außerhalb der Mitte: Crop **nur für diesen Beat** verschieben. Optionalen horizontalen Fokus pro Beat in der Content-Datei speichern (0 = linker Rand, 0,5 = Mitte, 1 = rechter Rand) und zwischen den Werten über die Beats weich interpolieren statt springen. Nur wenn der Crop nicht zu retten ist: notieren und die Stufen aus 4a anbieten – **nicht still neues Footage generieren.**

## 4a. Mobile-Stufen

Die Stufen legen nur fest, **welche Assets existieren**. Die Scroll-Animation und die Härtung aus Abschnitt 6 bekommen Handys in jeder Stufe.

| Stufe | Was entsteht | Kosten |
| --- | --- | --- |
| **1 – Crop** (Standard) | Nichts Neues. Desktop-Sequenz mit Cover-Fit und Fokus pro Beat. | keine |
| **2 – Mobile-Sequenz** | Vorgecroppte Hochformat-Sequenz aus demselben Master (siehe unten). Gleiches Bild, deutlich weniger Daten auf Mobilfunk. | keine Credits, nur Rechenzeit |
| **3 – Hero-Reframe** | Für die 1–2 Momente, deren Motiv keinen Crop verträgt (meist Eröffnung und Schluss-Luftbild): neue 9:16-Stills mit Start-Still bzw. Reveal-Still als Stil-Referenz. Sie dienen als Poster, Reduced-Motion-Bilder und Kapitelbilder im Stills-Modus – **nicht** als Ersatz für Frames mitten im Flug, sonst springt das Bild. | wenige Bild-Credits |
| **4 – Hochformat-Flug** | Ein kompletter zweiter Flug in 9:16: eigene Stills, eigene Extension-Kette, eigener SSIM-Check (aus `drone-fly`), eigene Sequenz. Seitenverhältnisse lassen sich innerhalb einer Kette nicht mischen, daher von vorn als eigener Take. | ≈ 2× Video-Credits des Desktop-Flugs |

- Stufe 1 und 2 ohne Rückfrage umsetzen. Stufe 2 ist der Normalfall, sobald die Sequenz auf Mobilfunk spürbar groß ist.
- Stufe 3 und 4 **nur anbieten**, wenn der Crop-Check scheitert oder der Nutzer betont, dass Mobile-Traffic wichtig ist. Vorher eine Kostenschätzung nennen und eine ausdrückliche Freigabe holen. Für Stufe 4 gelten alle Spend Gates aus `drone-fly` (Start-Still-Gate, Produktionslog, Budget-Stopp).

**Stufe 2 – Mobile-Sequenz extrahieren:** aus demselben Master (`crop=ih*9/16:ih` mit demselben Fokus pro Beat, native Auflösung, nie hochskalieren). Handys laden dann nur diese Sequenz. Gleiches Footage, sieht identisch aus, lädt weniger. Eigenes Poster = erster Frame **dieser** Sequenz, im Manifest als `posterMobile` neben `poster` eintragen.

## 5. Mobile-Scroll-Pacing

- Mobile-Timing unabhängig von Desktop. Die Beat-Timeline in der Content-Datei bekommt einen optionalen Mobile-Override für die Scroll-Strecke je Beat. Ohne Override gilt ein globaler Faktor `scrollMobileFactor` (Startwert 1,2: etwas mehr Strecke je Beat, weil Wischgesten Szenen schneller überfliegen als das Mausrad). Danach am Gerät justieren.
- Flug soll mit normalen Daumengesten in Bewegung bleiben. Standbild-Holds kürzen, dichten Innenmanövern genug Strecke geben, damit sie als Bewegung lesbar sind.
- 180°-Drehung bekommt einen eigenen kurzen Beat.
- Scroll-zu-Frame-Mapping anpassen statt Frames zu entfernen – Frames löschen allein verkürzt die Scroll-Strecke nicht.
- Kurze Holds am Anfang (Headline lesen) und Ende (Luftbild wirken lassen).
- Sichtbarer Link „Tour überspringen" zum Hauptinhalt.

## 6. Asset-Auslieferung und Performance

- Leichtes Poster (erster Frame) sofort zeigen. Frames progressiv um die aktuelle Scrollposition laden: aktuellen Frame zuerst, Vorladen in Scrollrichtung.
- Gleichzeitige Requests und dekodierten Speicher begrenzen, veraltete Requests bei schnellem Scrollen abbrechen, verdrängte Bitmaps freigeben (`bitmap.close()`). Frame-URLs mit der Manifest-Version cache-busten.
- Mit Hochformat-Sequenz: **vor** dem ersten Request die richtige Sequenz wählen – Handys nur Portrait, alle anderen nur Landscape. Nicht beide vorladen und eine per CSS verstecken. Bei einem echten Wechsel der Geräteklasse veraltete Requests abbrechen und Bitmaps der alten Sequenz freigeben.
- **Geräteklasse nach Bildschirmgröße bestimmen, nie nach Pointer-Typ oder User-Agent.** Handy = kürzere Bildschirmseite ≤ 600 CSS-px (`Math.min(screen.width, screen.height) <= 600`). iPads melden einen groben Pointer und teils einen Mac-User-Agent – nach diesen Signalen bekäme ein iPad Pro die kleine Handy-Sequenz. Tablets erhalten die Landscape-Sequenz mit Cover-Fit. Verhaltensanpassungen für Touch (Gesten, Hover-Ersatz) dürfen weiter an `pointer: coarse` hängen. Das ist eine andere Achse.
- **Data-Saver und langsames Netz nur als Herabstufung:** Chromium meldet `navigator.connection.saveData` und `effectiveType`, iOS meldet nichts davon. Deshalb ist die Standardauslieferung für alle sparsam (Poster zuerst, Frames nur im Fenster um die Scrollposition). Bei `saveData === true` in den Stills-Modus wechseln: Kapitel über Standbildern, Sequenz nicht laden. Bei `2g`/`3g` das Vorladefenster verkleinern. Nie umgekehrt (schwer laden und nur auf Signal sparen) – die meisten Handys im Mobilfunk sind iPhones und senden kein Signal.
- **iOS-Stromsparmodus:** Die Canvas-Bildsequenz läuft auch im Stromsparmodus, weil sie kein `<video>` braucht. Nutzt ein Projekt stattdessen Video-Scrubbing (`video.currentTime`), dann scheitert im Stromsparmodus selbst stummes `play()`. Das abgelehnte Promise beim ersten Touch erkennen und auf Stills mit Überblendungen umschalten, sonst bleibt der Flug eingefroren.
- Responsive Bildgrößen (`srcset`/`sizes`) auch für andere große Bilder (Stock, Lifestyle-Bänder).
- Seite nicht blockieren, bis die ganze Sequenz geladen ist; der Rest bleibt benutzbar.
- `prefers-reduced-motion`: komponierte Standbilder und normaler Seitenfluss, Sequenz gar nicht laden. Brauchbares Poster-Fallback bei Ladefehler.

## 7. Mobile-Layout für den Rest der Seite

Jede Sektion einspaltig umfließen statt das Desktop-Layout zu schrumpfen:

- Such-/Filterleisten: Felder volle Breite gestapelt, Primär-Button volle Breite.
- Kategorie-Tabs: umbrechen oder horizontal scrollen, ohne die Seite zu sprengen.
- Card-Grids: eine Spalte (zwei nur, wo Cards lesbar bleiben).
- Schritt-Abfolgen: vertikal stapeln, Verbindungslinien weglassen, die nicht mehr verbinden.
- Rechner, Slider, Formulare: Controls volle Breite, touch-taugliche Ziele.
- Bildbänder: Text nach unten über einen Scrim von unten.
- Footer-Spalten: auf zwei oder eine Spalte zusammenfassen.

## 8. Mobile-Validierung

Die echte Implementierung auf mehreren Handygrößen ansehen (Playwright `browser_resize` oder Chrome-Tools), z. B. 360 × 740, 375 × 812, 390 × 844, 430 × 932 – jeweils Hoch- und Querformat.

Prüfen:

- Eröffnungskomposition und sofortige Lesbarkeit.
- Center-Crop hält Türen, Kurven, Menschen und den Weg nach vorn über den ganzen Flug im Bild.
- Drehung und Schluss-Luftbild lesen sich im Crop.
- Scroll-Pacing durch Innenräume, Ausflug, Drehung, Reveal.
- Texte und Buttons bleiben vom Motiv frei.
- Glass-Header lesbar über den hellsten Frames; Wechsel zu Solid genau am Flugende – in beide Scrollrichtungen.
- Navigation bleibt nach dem Flug bestehen.
- Menü: öffnen, schließen, Fokus, Scroll-Lock, Anker-Offsets.
- Safe-Area-Abstände, kein horizontaler Overflow in keiner Sektion.
- Reduced-Motion- und Ladefehler-Verhalten.
- **Tablet:** iPad-Viewport (834 × 1194, Touch) lädt die **Landscape**-Sequenz, nicht die Handy-Sequenz.
- **Data-Saver:** mit emuliertem `navigator.connection.saveData = true` (Init-Script in Playwright) erscheint der Stills-Modus, und es werden keine Frames angefragt.
- Bei Stufe 4: SSIM-Check des Hochformat-Flugs liegt vor, alle Übergänge PASS oder per Crossfade gelöst.

**Danach Desktop erneut prüfen**, inklusive beider Header-Zustände.

Wenn Netzwerk-Inspektion verfügbar ist: nachsehen, welche Frame-Assets jeder Viewport tatsächlich lädt. Gemessene Asset-Größen getrennt von echten Ladezeit-Messungen berichten – keine Geschwindigkeit aus Dateigröße allein versprechen. Durchgeführte und nicht durchgeführte Checks klar trennen.

Am Ende eine Mobile-Preview bereitstellen und erklären: Mobile und Desktop sind responsive Varianten derselben Website mit demselben Fly-through-Footage, je Screen passend gerahmt.
