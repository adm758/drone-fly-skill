# drone-fly – Claude-Code-Skills

Zwei Skills für Claude Code, mit denen du eine Marken-Website rund um einen cineastischen FPV-Drohnenflug durch ein Firmengebäude baust. Scrollen steuert die Kamera vor und zurück.

| Skill | Wofür |
|---|---|
| `drone-fly` | Baut die komplette Website (Desktop) mit dem durchgehenden Drohnenflug. Bilder und Clips über Higgsfield MCP, Schnitt über FFmpeg. |
| `drone-fly-mobile` | Optimiert eine fertige drone-fly-Website fürs Smartphone, im selben Projekt. |

## Installation

### Einfachste Variante: Claude machen lassen

Gib Claude Code diesen Satz:

> Installiere die Skills aus https://github.com/GoldsteinBauGmbH/drone-fly-skill nach ~/.claude/skills

### Manuell

```bash
git clone https://github.com/GoldsteinBauGmbH/drone-fly-skill.git /tmp/drone-fly-skill
mkdir -p ~/.claude/skills
cp -R /tmp/drone-fly-skill/skills/drone-fly ~/.claude/skills/
cp -R /tmp/drone-fly-skill/skills/drone-fly-mobile ~/.claude/skills/
```

Danach Claude Code neu starten.

## Benutzung

- `/drone-fly` startet den Bau der Website.
- `/drone-fly-mobile` macht die fertige Website anschließend handytauglich.

## Voraussetzungen

- Claude Code
- Higgsfield-Connector (MCP) für Bilder und Videoclips
- FFmpeg (`brew install ffmpeg` auf dem Mac)
