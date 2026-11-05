# SDK — INSTRUMENT.TestSet

Every TestSet model this library drives, and how to drive it. Each model answers the same five verbs over HTTP (its own port), WebSocket, a Unix socket and the bus; one page per model below lists its routes and every command.

← [Manual and Artifacts](INDEX.md)

| Verb | What it does |
|---|---|
| `get` | reads one value |
| `set` | writes one value |
| `nab` | reads more than one thing (observation, telemetry) |
| `rig` | configures several arguments at once |
| `do` | executes an action; takes no value |

| Model | Maker | get | set | nab | rig | do | Port |
|---|---|---:|---:|---:|---:|---:|---:|
| [8960](SDK/8960.md) | HP / Agilent / Keysight | 22 | 7 | 22 | 2 | 5 | 16300 |
| [E5515C](SDK/E5515C.md) | HP / Agilent / Keysight | 22 | 7 | 22 | 2 | 5 | 16301 |
| [E5515E](SDK/E5515E.md) | HP / Agilent / Keysight | 22 | 7 | 22 | 2 | 5 | 16302 |
| [Virtual_TestSet](SDK/Virtual_TestSet.md) | APK.audio | 10 | 3 | 10 | 1 | 6 | 16303 |
