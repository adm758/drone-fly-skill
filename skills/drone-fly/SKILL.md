---
name: drone-fly
description: Baut eine komplette Marken-Website rund um einen cineastischen FPV-Drohnenflug durch das Gebäude eines Unternehmens – ein durchgehender Take, der zur Vordertür hinein, durch alle Räume, hinten hinaus fliegt, sich um 180° dreht und steigend das ganze Gelände zeigt. Scrollen steuert die Kamera vor und zurück. Bilder und Clips kommen über Higgsfield MCP, Schnitt und Frames über FFmpeg. Verwenden bei "/drone-fly", "Drohnenflug-Website", "Fly-through-Website", "FPV-Website", "Website mit Kamerafahrt durchs Gebäude". Für die Handy-Version danach `drone-fly-mobile` nutzen.
---

# Drone Fly – Desktop-Website mit Fly-through

Du arbeitest als Designer, Creative Director und Webentwickler zugleich. Ergebnis ist die fertige Website inklusive Assets und funktionierender Scroll-Animation – kein Konzeptpapier.

Herzstück: **ein einziger durchgehender First-Person-Flug** durch den Betrieb. Die Kamera schneidet nie und springt nie zwischen Räumen. Jeder Raumwechsel passiert physisch: durch eine Tür, um eine Ecke, durch eine Öffnung. Die Route ist die Geschichte.

## 0. Werkzeuge prüfen, bevor du etwas versprichst

- **Higgsfield MCP** (`mcp__claude_ai_Higgsfield__*`) ist der Standard für Bilder und Video. Vor der ersten Generierung prüfen, ob die Tools aufrufbar sind. Fehlen sie, die Lücke einmal konkret benennen, um die kleinste nötige Aktion bitten und parallel an unabhängigen Teilen (Design, Code) weiterarbeiten.
- Nicht stillschweigend auf einen anderen Anbieter ausweichen. Wenn der Nutzer ausdrücklich über API-Guthaben statt Plan generieren will, `/hgf` anbieten; kie.ai nur auf Wunsch.
- **FFmpeg** muss vorhanden sein (`which ffmpeg`). Fallback ohne Homebrew: `npm install -g ffmpeg-static`.
- Keine Abos kaufen, keine Kontoeinstellungen ändern. Das Erstellen von Assets autorisiert nur das Verbrauchen von Credits im abgesprochenen Rahmen. Wie dieser Rahmen festgelegt und eingehalten wird, regeln die **Spend Gates** (Abschnitt 1 und 4).

## 1. Briefing mit wenig Reibung

Erst Gespräch und mitgelieferte Unterlagen lesen. Nur fragen, was das Ergebnis wirklich verändert. Wenn etwas fehlt, eine kompakte Rückfrage:

- Was macht der Betrieb, für wen, und was sollen Besucher auf der Seite tun?
- Gibt es Name, Logo, Farben, Brand Guidelines?
- Referenz-Websites oder eine Beschreibung der gewünschten Anmutung?
- Welche Route? Welche Räume soll die Kamera durchfliegen (Eingang, Showroom, Werkstatt, Lager, Hof …) und wo kommt sie raus?

Keine bereits beantworteten Fragen wiederholen. Eine Geschäftsbeschreibung reicht zum Starten. Fehlt die Route, eine realistische für diese Art von Betrieb vorschlagen.

**Zwei Modi:**

- **Geführt:** wenige, sinnvolle Freigabepunkte – Budget, Stilrichtung, Start-Still, Flugroute. Konkrete Optionen zeigen statt abstrakt fragen. Nach der Entscheidung weitergehen.
- **Autonom/Template:** Bei „mach einfach", „entscheide du", „bau ein Template" o. ä. passende Defaults wählen und ohne Warten durchbauen. Fehlende Texte blockieren nicht: sauberes, leicht austauschbares Content-Gerüst, Annahmen im Handoff festhalten.

Echte Fakten übernehmen. **Nichts erfinden**: keine Testimonials, Kunden, Auszeichnungen, Adressen, Jahre Erfahrung, Projektzahlen. Bei Demo-/Template-Betrieben den Demo-Status klar machen und brauchbare Platzhalter setzen.

### Budgetstufe und Kostenfreigabe (Spend Gate 1)

Videojobs machen den Großteil der Kosten aus. Deshalb die Budgetstufe **vor** dem Entwurf der Route klären – sie bestimmt, wie viele Segmente und Räume der Flug bekommt. Ist schon ein Credit-Rahmen genannt, daraus ableiten statt fragen.

| Stufe | Flug | Richtwert |
| --- | --- | --- |
| **Schlank** | 2 Segmente (Ankunft + Hauptraum → Ausflug + Reveal), 3–4 Räume, keine Vorschau-Runde | ≈ 350–450 Credits |
| **Standard** | 3 Segmente wie in Abschnitt 4 beschrieben | ≈ 600–700 Credits |
| **Showcase** | 3 Segmente plus Vorschau-Runde (Previz) und optional Hochformat-Stufen aus `drone-fly-mobile` | ≈ 900+ Credits |

Weniger Segmente heißt nicht weniger Wirkung: Bei der schlanken Stufe bekommen die verbleibenden Beats mehr Scroll-Strecke, damit der Flug trotzdem vollständig wirkt. Richtwerte vor dem Nennen mit dem Live-Preis des Modells abgleichen (Vorabprüfung des Tools, `balance`).

**Das Briefing endet mit einer Kostenschätzung und einer ausdrücklichen Freigabe – vor dem ersten Bild- oder Videojob.** In konkreten Zahlen: Anzahl Stills, Anzahl Videojobs, Puffer für Reparaturen (~20–30 %, Innenräume und Content-Filter kosten Wiederholungen), grobe Laufzeit. Das gilt **auch im Autonom-Modus**: einmal die Schätzung nennen und das Go abholen, danach ohne weitere Rückfragen durchbauen. Nach dieser Freigabe gibt es nur noch zwei Stopps, und beide schützen das große Budget: das Start-Still-Gate (Abschnitt 4) und – bei Showcase – die Previz-Abnahme.

## 2. Identität und Style Tile

- Vorhandenes Logo und offizielle Assets unverändert übernehmen. Ein bestehendes Logo nie „passend umzeichnen". Inspiration und eigenes Material des Nutzers auseinanderhalten.
- Fehlt eine Identität: ein paar passende Richtungen entwickeln, Logo-Konzepte über Higgsfield erzeugen. Im Autonom-Modus das stärkste nehmen, sonst kompakt zur Wahl stellen. Wenn möglich einen editierbaren Vektor-Master; ein Raster-Export ist kein SVG-Master.
- Referenz-Websites erst ansehen, dann beschreiben. Typografie, Abstände, Kontrast, Komposition, Materialien, Komponenten, Motion extrahieren – keine fremden Marken oder markanten Artworks kopieren.
- Ohne Referenzen eine stimmige Richtung aus dem Geschäft ableiten. Nicht jeden Betrieb in dasselbe Template pressen.
- **Style Tile** als editierbare HTML/CSS-Seite mit den echten Design-Tokens: Logo, Farbpalette, Heading-/Body-Schrift, Buttons, Links, eine Beispiel-Card, Bildsprache. Kein Screenshot der fertigen Seite, kein ganzes Brandbook.
- Eine Identität über Board, Assets und Website hinweg. Quell-Assets, Prompts und Auswahlbegründung aufbewahren.

## 3. Flugroute entwerfen

### Visual-Story-Tabelle (vor jeder Videoproduktion zeigen)

Genau drei Spalten: **Scene**, **Visual story**, **Website copy**. Jede Zeile ist ein Streckenabschnitt; konkrete, betriebsspezifische Textvorschläge statt leerer Platzhalter. Beispielstruktur:

| Scene | Visual story | Website copy |
| --- | --- | --- |
| 01 — Ankunft | Außen auf Augenhöhe anfliegen, im Bogen an einem markanten Objekt vorbei, auf den offenen Eingang ausrichten, hineingleiten. | Hero-Headline, Unterzeile, Primär-CTA |
| 02 — Hauptraum | Abbremsen, an der Seite des Hero-Produkts entlang, S-Kurve um ein zweites, Blick quer durch den Raum. | Angebot: Headline, Text, CTA |
| Übergang — Tür | Mitarbeiter öffnet eine Tür, Kamera fliegt direkt hindurch. | Kein Text – Bewegung führt |
| 03 — Hinter den Kulissen | Bogen um die laufende Arbeit, abtauchen für Nähe, an Geräten vorbeikurven. | Service/Handwerk: Headline, CTA |
| 04 — Lager / Weg nach draußen | Durch Seitentür, Gang entlang schlängeln, am Ende abbiegen, um die Ecke zur Ausgangsöffnung. | Unterstützende Headline |
| Übergang — Ausflug und Drehung | Hinten hinaus, weiter in Bewegung, dann 180°-Gier zum gerade verlassenen Gebäude. | Kein Text – Bewegung führt |
| 05 — Reveal | Rückwärts fliegen und steigen, das ganze Gelände samt Straßen und Umgebung zeigen. | Abschluss-Headline, Betriebsinfos, Abschluss-CTA |

Zeilen an den Betrieb anpassen. Danach kurz erklären, wie die Route läuft und wie Scrollen den Text einführt, hält und wieder entfernt.

### Wie ein echter Pilot fliegen

Gerade Schienenfahrt wirkt wie ein Kamerawagen, nicht wie eine Drohne. Deshalb:

- **Tempo variieren:** langsam bei Details, schnell durch Übergangsräume.
- **Banken und seitlich driften:** im Bogen an Objekten vorbei, damit ihr Profil sichtbar wird, dann zurückkurven.
- **Gieren zum Umschauen:** Blick zu Produkt, Techniker, Fensterausblick drehen, während die Kamera weiterfliegt.
- **S-Kurven** in offenen Räumen und um Hindernisse.
- **Gebäudelogik respektieren:** Innenräume sind kein gerader Korridor. Realistische Abbiegungen planen.
- **Manöver zeitlich takten** mit Sekundenbereichen („3–7 s: bremst ab, bankt links, giert rechts an der ganzen Seite von …").

### Ausflug und Reveal physikalisch korrekt

- Durch die Hintertür sieht man, was wirklich hinten liegt (Hof, Zufahrt, Zaun, Himmel) – nicht die Vorderseite desselben Gebäudes.
- Um das verlassene Gebäude zu zeigen: **während der Bewegung um 180° gieren**, dann **rückwärts fliegen und steigen**. Nie vorwärts hinausfliegen und dasselbe Gebäude vor sich sehen.
- Das Schlussbild verortet den Betrieb realistisch: Zufahrt, Parkplatz/Vorplatz, Hauptstraße mit Verkehr, Nachbargebäude. Nie allein auf einer leeren Wiese.
- Architektur konsistent zum Start-Still: gleiche Materialien, Rahmen, Verglasung, Maßstab.

### Scroll-Pacing

Unter der Tabelle ein knapper Plan je Szene/Übergang: was ein-/ausgeblendet wird, aktive Scroll-Strecke in Viewport-Höhen (vh), kontinuierliche Bewegung oder Standbild-Hold.

- Eröffnungsframe lang genug halten, um die Hero-Copy zu lesen.
- Dichte Innenmanöver bekommen mehr Strecke.
- Schnelle Gier/Drehung bekommt einen eigenen kurzen Beat, damit sie nicht wie ein Sprung wirkt.
- Schluss-Luftbild am Ende halten.
- Scroll-Strecke unabhängig von Clipdauer und Frameanzahl vergeben, in vh messen (nicht in Mausrad-Rasten).
- **Stückweise Timeline:** jeder Beat bildet sein Scroll-Intervall auf sein Frame-Intervall ab; ein Hold bildet ein Intervall auf genau einen Frame ab. Gepinnte Scroll-Strecke getrennt von der Höhe der sichtbaren Bühne zählen.

Geführt: Tabelle und Erklärung zur Freigabe zeigen, bevor Footage entsteht. Autonom: trotzdem zeigen, dann ohne Warten weiter.

Responsive Komposition schon jetzt mitdenken: Platz für Text reservieren, wichtige Aktion nicht an die äußersten Bildränder legen (Mobile croppt später auf die Mitte).

## 4. Den Flug als einen verketteten Take erzeugen

Vor dem Absenden das Live-Schema des Modells prüfen: Dauergrenzen, Seitenverhältnis, Auflösung, Referenzrollen, verfügbare Modi. Bei unklarer Modellwahl `models_explore(action:'recommend')`.

### Erst Stills

1. **2–3 Start-Stills** in unterschiedlichen Richtungen: Außenansicht auf Augenhöhe, Eingangstüren offen, lädt die Kamera ein. Eins wählen (oder wählen lassen). Das wird der exakte erste Frame.
2. **Start-Still-Gate (Spend Gate 2):** Erst wenn das Start-Still steht, geht es weiter. Geführt: Freigabe abwarten. Autonom: selbst entscheiden, Begründung in die Production Note. Ein verworfener Stil kostet hier ein paar Stills statt eines ganzen Flugs – deshalb nie Video starten, solange die Richtung offen ist. Bei Ablehnung den Stil-Teil des Prompts für **alle** folgenden Prompts korrigieren, nicht nur für dieses Bild.
3. **Reveal-Referenz-Still** aus dem freigegebenen Start-Still ableiten (Start-Still als Bildreferenz für Stil und Architektur): hohe Luftaufnahme auf die Rückseite desselben Gebäudes mit Ausgangsöffnung, Hof, ganzem Gelände, angebundenen Straßen. Das ist Zielbild für den Schluss und hält die Architektur konsistent.

In Prompts keine echten Marken, Logos oder markante Trade Dress (z. B. echte Automarken): Produkte ohne Emblem, keine Schriftzüge auf Schildern.

### Verketten mit Extension, nicht mit Einzelszenen

Route in 2–3 Segmente à max. ~15 s teilen, damit jedes Manöver Zeit bekommt:

- **Clip A:** Image-to-Video (z. B. Seedance 2.5 `omni_reference`) mit dem Start-Still als `start_image` – Eingang und Hauptraum.
- **Clip B:** **Video-Extension**-Modus (z. B. Seedance 2.5 `video_extension`, `extension_mode: forward`) mit Clip A als Referenzvideo – Hinterräume und Lager.
- **Clip C:** Extension von Clip B plus Reveal-Still als Bildreferenz – Ausflug, 180°-Gier, Rückwärts-Steigflug.

Extension führt Kamera, Licht und Tempo vom letzten Frame des Vorgängers fort – deshalb wirkt der Flug ununterbrochen. Keine unabhängigen Szenen erzeugen und auf eine Überblendung hoffen.

Segmente der Reihe nach erzeugen und jedes prüfen, bevor das nächste startet. Ein laufender Job ist kein gescheiterter Job. Während Clips rendern, an der Website weiterbauen.

### Nie doppelt bezahlen (Spend Gate 3)

- **Produktionslog** im Projekt führen, z. B. `production/jobs.json`: pro Asset Name, Modell, Prompt-Datei, Job-ID, Status, lokaler Pfad, Credits laut Vorabprüfung und laut `balance`-Differenz.
- **Vorhandene Ergebnisse gelten als erledigt.** Vor jedem Absenden prüfen: Liegt die Datei lokal schon vor, oder hat der Job laut Log eine ID? Dann erst `jobs_wait` / `show_generations` abfragen statt neu abzusenden. So kostet ein abgebrochener Lauf oder ein Session-Wechsel nichts doppelt.
- Eine bewusste Neugenerierung nur nach Eintrag im Log (Grund, alte Job-ID) – nie still.
- **Budget-Stopp:** Nach jedem Videojob `balance` prüfen. Liegt der tatsächliche Verbrauch mehr als ~20 % über der freigegebenen Schätzung, anhalten, Stand und Grund nennen und eine neue Freigabe holen, bevor der nächste Job startet.

### Previz bei Showcase (optional)

Bei der Showcase-Stufe lohnt eine Vorschau-Runde: den ganzen Flug zuerst auf einer günstigen Draft-Stufe erzeugen, Route, Manöver, Übergänge und Scroll-Pacing an der fertig gebauten Seite abnehmen, erst danach mit dem vollen Modell rendern. Voraussetzung: Die Draft-Stufe beherrscht **denselben Modus** (Start-Frame und Video-Extension) – per `models_explore` bzw. Live-Schema prüfen. Ein Modell ohne Extension taugt nicht als Previz, weil sich seine Übergänge nicht übertragen lassen. Die Stills werden unverändert weiterverwendet, nur die Videojobs laufen neu. Bei Schlank und Standard ist eine gezielte Reparatur meist billiger als eine zweite Runde – dort Previz weglassen.

### Prompt-Formulierung, die zählt

- **Nie „drone", „quadcopter", „UAV" (oder „Drohne") in einen Video-Prompt schreiben.** Sonst zeichnet das Modell eine Drohne ins Bild. Stattdessen die Kamera beschreiben: „one single continuous first-person camera move, no cuts; the camera itself is flying; nothing flying or hovering is ever visible in frame."
- „every vehicle/person/object is stationary unless described; nothing appears, disappears or changes" – damit nichts auftaucht oder verschwindet.
- Jedem Segment getaktete Manöver geben und sagen, was durch die nächste Öffnung zu sehen ist.
- Licht (warm/kalt), Objektiv-Look und „no text, no logos, no brand badges, no signage lettering" angeben.
- Schlägt die Plattform ein unpassendes Preset vor: ablehnen und den Prompt wörtlich generieren.

### Jeden Clip prüfen (FFmpeg)

- Kontaktabzug mit 1–2 fps erzeugen und ansehen:
  `ffmpeg -i clip.mp4 -vf "fps=1,scale=480:-1,tile=6x3" -frames:v 1 contact.jpg`
- Schnitterkennung, um versteckte Cuts auszuschließen:
  `ffmpeg -i clip.mp4 -vf "select='gt(scene,0.3)',showinfo" -f null - 2>&1 | grep pts_time`
- In die letzten Sekunden und jede Tür/Kurve hineinzoomen.
- Jeden Übergang zwischen zwei Clips maschinell prüfen (SSIM-Check, siehe unten) – vor dem Anschauen mit bloßem Auge.

Suchen nach: Drohnen oder fliegenden Objekten im Bild, Autos/Personen aus dem Nichts, Logos, unrealistischer Geografie, Sprüngen in Position, Maßstab oder Licht.

### SSIM-Check an jedem Übergang

Nahtlosigkeit ist das Produkt – nicht nach Augenmaß abnehmen. Bei Extension ist der erste Frame von Clip B der **nächste** Frame nach Clip A, nicht derselbe. Deshalb wird der Übergang relativ zur normalen Bewegung gemessen: Der Schritt A→B soll so ähnlich ausfallen wie der Schritt zwischen den letzten beiden Frames von A. Feste Schwellen allein würden schnelle Gier-Bewegungen fälschlich als Sprung werten.

```sh
ssim_pair() { # bildA bildB → SSIM-Wert (All)
  ffmpeg -v info -i "$1" -i "$2" \
    -lavfi "[0:v]scale=960:540,format=yuv420p[a];[1:v]scale=960:540,format=yuv420p[b];[a][b]ssim" \
    -f null - 2>&1 | grep -o 'All:[0-9.]*' | tail -1 | cut -d: -f2
}
seam_check() { # clipA clipB label
  T=$(mktemp -d)
  ffmpeg -v error -sseof -0.5 -i "$1" "$T/a%03d.png"
  a_prev=$(ls "$T"/a*.png | tail -2 | head -1); a_last=$(ls "$T"/a*.png | tail -1)
  ffmpeg -v error -i "$1" -frames:v 1 "$T/a_first.png"
  ffmpeg -v error -i "$2" -frames:v 1 "$T/b_first.png"
  base=$(ssim_pair "$a_prev" "$a_last")               # normale Bewegung am Ende von A
  seam=$(ssim_pair "$a_last" "$T/b_first.png")        # Übergang A→B
  dup=$(ssim_pair "$T/a_first.png" "$T/b_first.png")  # liefert B das Eingangsvideo mit?
  awk -v s="$seam" -v b="$base" -v d="$dup" -v l="$3" 'BEGIN{
    r = (b > 0) ? s/b : 0
    if (d >= 0.95 && d > s) v = "FAIL  " l "  B beginnt mit dem Anfang von A – Extension liefert das Eingangsvideo mit; Überlappung vor dem Concat abschneiden"
    else if (s >= 0.90 || r >= 0.92) v = "PASS  " l
    else if (s < 0.75 && r < 0.80) v = "FAIL  " l "  Sprung am Übergang – trimmen/reparieren (Abschnitt Reparieren)"
    else v = "WARN  " l "  Crossfade 0,125 s setzen und Übergang ansehen"
    printf "%s  ssim=%.3f  bewegung=%.3f  verhältnis=%.2f  anfang=%.3f\n", v, s, b, r, d }'
  rm -rf "$T"
}

seam_check clip-a.mp4 clip-b.mp4 "A>B"
seam_check clip-b.mp4 clip-c.mp4 "B>C"
```

- **PASS** (SSIM ≥ 0,90 oder ≥ 92 % der normalen Bewegung): harte Concat.
- **WARN**: kurzer Crossfade (`xfade` 0,125 s), Übergang im Kontaktabzug ansehen.
- **FAIL Sprung**: nicht schönreden. Auf saubere Frames trimmen oder reparieren (nächster Abschnitt), dann erneut prüfen.
- **FAIL Überlappung**: Clip B enthält das Eingangsvideo. Die Länge von A vom Anfang von B abschneiden, dann erneut prüfen.

Den Check auf die **normalisierten** Segmente anwenden, die tatsächlich in den Master gehen. Nach jeder Reparatur, jedem Edit und jedem eingesetzten Stück erneut laufen lassen: Ein ersetztes Stück berührt **beide** Übergänge. Ergebnisse in die Production Note.

### Reparieren statt neu generieren

Eine Extension komplett neu zu erzeugen ist teuer. Gezielt reparieren:

- **Auf saubere Frames trimmen:** Artefakt spät im Clip → davor schneiden, getrimmte Datei hochladen (`media_upload`, Bytes per PUT, `media_confirm`) und von der getrimmten Version aus extenden.
- **Kleine Artefakte wegeditieren:** betroffenes Stück ausschneiden, per Text-Video-Edit bearbeiten (z. B. FLUX 3 Video Edit: „remove the small flying quadcopter from every frame; keep everything else identical") und wieder einsetzen. Edits kommen evtl. in niedrigerer Auflösung zurück – weichere Stelle notieren. Logo-Entfernung kann vom Content-Filter blockiert werden, daher Anweisung auf die Objektentfernung beschränken.
- **Von einem sauberen Ende weiter extenden**, wenn nur der Anfang repariert wurde.

Keine offene Neugenerierungsschleife. Brauchbare Assets behalten.

### Einen Master zusammensetzen

- Alle Segmente auf gleiche Größe, Framerate, Pixelformat bringen: `scale=1920:1080:flags=lanczos,fps=24,format=yuv420p,setsar=1`
- Übergänge mit PASS per **harter Concat** verbinden.
- Übergänge mit WARN sowie Stellen, an denen ein editiertes Stück auf ein Original trifft: sehr kurzer **Crossfade** `xfade=transition=fade:duration=0.125`.
- Kein Übergang mit FAIL im Master.
- Schnitterkennung auf dem Master wiederholen, Kontaktabzug des ganzen Flugs ansehen.

Tatsächlichen Credit-Verbrauch im Produktionslog festhalten. Extension-Jobs können mehr kosten als die Vorabprüfung anzeigt (sie verarbeiten auch das Eingangsvideo) – deshalb gilt der Budget-Stopp aus Spend Gate 3.

### Frame-Sequenz vorbereiten

In ein frisches Staging-Verzeichnis extrahieren:

```sh
mkdir -p frames
ffmpeg -i flythrough-master.mp4 -an -vf "fps=20,scale=1440:-2:flags=lanczos" -c:v libwebp -quality 78 -start_number 0 frames/frame-%04d.webp
```

18–24 fps nutzen – höhere Raten halten schnelle Gier und Drehungen beim Scrubben flüssig. Größe/Qualität an die gemessene Transfergröße anpassen.

**Poster = `frame-0000` der Sequenz, nicht das Start-Still.** Das Start-Still hat einen anderen Bildausschnitt und ein anderes Rendering als der erste Videoframe. Als Ladeposter erzeugt es genau beim ersten Eindruck einen sichtbaren Sprung, sobald die Sequenz übernimmt. Das Start-Still bleibt Artwork für Reduced-Motion und Fallbacks.

**Manifest** schreiben mit tatsächlicher Anzahl, fps, Maßen, Namensmuster, Poster und einem Versionswert zum Cache-Busting der Frame-URLs. Ersten, mittleren und letzten Frame sowie alle referenzierten Pfade vor der Integration prüfen.

## 5. Vollständige, benutzbare Website bauen

- Bestehendes Projekt und passende Komponenten wiederverwenden. Vorgegebenen Build-/Deploy-Workflow der Umgebung einhalten.
- Nicht nur Animation: sinnvolle Navigation, klares Angebot, relevante Sektionen, Primär-CTA.
- Fly-through als **gepinnte Canvas-Bühne**. Scroll → Frames über die stückweise Beat-Timeline. Jeder Beat steht in einer editierbaren Content-Datei (`vh`, Clip-`from`/`to` in Sekunden, welches Text-Kapitel er trägt). Copy blendet innerhalb ihrer Beats ein, hält, blendet aus; erstes Kapitel ist im Ruhezustand sichtbar, letztes hält am Ende.
- Motion-Rendering strikt von semantischem HTML trennen. Texte, Buttons, Navigation bleiben scharf, markierbar, barrierefrei, editierbar.
- **Kein Scroll-Hijacking**: natives Scrollen vor- und rückwärts. Ausgeblendete Copy fängt keine Klicks ab und ist nicht in der Tab-Reihenfolge. Link „Tour überspringen" anbieten.
- Frame-Loading: angefragten Frame und Nachbarn in Scrollrichtung priorisieren. Gleichzeitige Requests und dekodierten Speicher begrenzen, veraltete Requests abbrechen, verdrängte Bitmaps freigeben, begrenzte Retries. Schnelle Sprünge, Rückwärtsscrollen, Resize und HiDPI abdecken. Poster zeigen, solange Frames laden.
- Header lesbar über der dunklen Bühne und über hellen Sektionen danach.
- Fallbacks für `prefers-reduced-motion` und schwache Geräte: jedes Kapitel über einem repräsentativen Standbild. Das Geschäft muss ohne Animation verständlich sein.
- Mobile umfließen statt verkleinern – die Feinarbeit macht danach `drone-fly-mobile`.

## 6. Austauschbar halten, prüfen, übergeben

- Business-Texte, Leistungen, CTAs, Beat-Timeline und Medienreferenzen in einer klaren Content-Datei (oder vorhandenem CMS).
- Formulare brauchen ein echtes Ziel oder ein klar beschriftetes Demo-Verhalten. Nie „gesendet" anzeigen, wenn nichts gesendet wurde.
- Code-, Build- und Asset-Checks laufen lassen. Manifest, Frame-Pfade, Poster prüfen. Flug auf Desktop- und Handy-Größe testen (Playwright oder Chrome-Tools, soweit erlaubt): jeder Beat trifft seinen Frame, Kapitel erscheinen auf ihren Beats, Schluss-Hold funktioniert, kein horizontales Scrollen. Wenn Interaktionstests nicht möglich sind, offen sagen, dass das Pacing ungeprüft ist.
- Durchgeführte und nicht durchgeführte Checks klar trennen.
- Nur im freigegebenen Rahmen veröffentlichen, keinen Entwurf still öffentlich machen. Ohne Publishing ein lauffähiges lokales Projekt liefern und die fehlende Abhängigkeit nennen.

**Lieferumfang:** Website/Preview, Style Tile, Logo-Master, Start- und Reveal-Still, Original-Clips, gestitchter Master, editierbarer Content, kurze Bearbeitungsanleitung. Dazu eine **Production Note**: gewählte Richtung, Budgetstufe, Route, Prompts, Job-IDs (aus dem Produktionslog), Reparaturen, geschätzte vs. verbrauchte Credits, SSIM-Ergebnisse je Übergang, wichtige Messwerte, beobachtete Grenzen. Keine Zugangsdaten und keine temporären signierten URLs in wiederverwendbaren Paketen.

Weitermachen, bis das Ergebnis fertig ist oder eine konkrete Abhängigkeit blockiert. Fortschritt und fertige Ergebnisse zeigen statt wiederholter Pläne.

## Vor dem Launch (Hinweis an den Nutzer)

Geschäftsinfos, Texte, Links und CTA prüfen. Beispielinhalte (Stock, Preise, Bewertungen, Öffnungszeiten) durch echte ersetzen. Nie erfundene Bewertungen für einen echten Betrieb veröffentlichen. Formulare auf ein funktionierendes Ziel prüfen.

Nächster Schritt: `drone-fly-mobile` im selben Projekt und Gespräch ausführen.
