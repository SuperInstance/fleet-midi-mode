🎼 **fleet-midi-mode** — Musical mode detection from agent state patterns

Identifies modal centres (Ionian, Dorian, Phrygian, Lydian, Mixolydian, Aeolian, Locrian) from agent activation vectors. Detects borrowed chords, modal interchange, and tonal drift. Part of the SuperInstance MIDI fleet.

---

## Wait, show me

```bash
# Analyse a mode from pitch content
fleet call mode --notes 62,64,66,67,69,71,73
# → D Dorian (D E F G A B C)

# Detect mode from a chord progression
fleet call mode --chords "Cmaj7 Dm7 G7"
# → C Ionian (major), with brief Mixolydian on G7

# Or hit the raw API
curl -s 'http://localhost:2162/mode?notes=60,62,63,65,67,68,70' | jq .
{
  "notes":    [60, 62, 63, 65, 67, 68, 70],
  "root":     "C",
  "mode":     "aeolian",
  "familiar": "C natural minor",
  "quality":  "minor"
}
```

**6‑language verification** — every response carries this fingerprint confirming the mode agent is live:

```
[60, 64, 64, 60, 64, 64, 60, 64, 68]
```

This sequence encodes a C-E-E-C-E-E-C-E-G♯ arpeggiation — a C Ionian pattern resolving to a raised fifth — the mode agent's heartbeat signature. If you don't see it, the agent isn't running.

---

## Where this fits

The SuperInstance MIDI fleet turns fleet agent state into living music. Each repo is a lightweight ensign agent that owns one musical dimension:

| Agent | Repo | Domain |
|-------|------|--------|
| Chord | `SuperInstance/fleet-midi-chord` | Harmony & voicing |
| Scale | `SuperInstance/fleet-midi-scale` | Pitch collections |
| **Mode** | `SuperInstance/fleet-midi-mode` | Modal analysis |
| Tempo | `SuperInstance/fleet-midi-tempo` | BPM & timing |

Routed together through the fleet conductor, they produce real-time MIDI from ternary agent states.

🔗 [fleet-midi-chord](https://github.com/SuperInstance/fleet-midi-chord) · [fleet-midi-scale](https://github.com/SuperInstance/fleet-midi-scale) · [fleet-midi-tempo](https://github.com/SuperInstance/fleet-midi-tempo)
