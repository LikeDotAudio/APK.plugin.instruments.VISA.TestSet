# Virtual_TestSet — TestSet

← [SDK](../SDK.md)

**APK.audio** — APK.audio Virtual Test Set (Synthesized RF + Audio Multi-Function Emulator)

| | |
|---|---|
| Family | `TestSet` |
| Channels | 2 |
| Spec | `GET /api/instrument/TestSet/Virtual_TestSet` |
| Default transport | `raw_socket` |
| Ranges | `rf_freq` 100000000…3000000000 Hz; `rf_power` -130…30 dBm; `audio_freq` 10…50000 Hz; `thd_n` 0.0001…100.0 %; `sinad` 0…120 dB |
| Reference | [commands tree](../../../Virtual_TestSet/commands_tree.md) · [sources](../../../Virtual_TestSet/SOURCES.md) |

<!-- sdk:io -->
## Inputs and outputs — the box

No part for this model in the BIM library yet (`DATABASE.server.BIM`), so its connectors are not stated here. Add the part there — the one place a device type is described — and regenerate.

<!-- /sdk:io -->

## Driving it

Three doors, all on the bench's own services — none of them is a per-model process.

1. **The bus, through KOMAND** (what a panel and the touch pad do). Teach the topic its handler, then send the value; never retained — KOMAND ignores a retained value on purpose. `target` is the box's Write topic (`GET /api/instrument/status?protocol=visa&resource=…` → `write_topic`); a DO/NAB fires on a truthy value.

```sh
T=APK.audio/Gui/MyPanel/Set_Audio_Freq
mosquitto_pub -t "$T/config" -m '{"komand_handler": {"enable": true, "komand_type": "set", "command": "Set_Audio_Freq", "model": "Virtual_TestSet", "input_name": "value", "target": "<box>/Write"}}'
mosquitto_pub -t "$T" -m '{"value": <value>}'
```

2. **Raw SCPI** — `POST /api/instrument/send` with `{"protocol": "visa", "resource": "<VISA resource>", "command": "<SCPI>"}`; the answer comes back in the reply and on `<box>/Read`.

3. **The spec, over HTTP** — `GET /api/instrument/TestSet/Virtual_TestSet` (this model's whole `api.json`), `GET /api/instrument/TestSet/Virtual_TestSet/<verb>/<command>` (one command's entry), `GET …/health`. These describe; they do not send anything to the box.

A read's answer is published on `<box>/Reading/<command>` (the **Out** column below); `<box>` is `APK.audio/System/Protocols/visa/Device/<Family>/<Model>/<Dev…>`.

## Commands (30) — inputs and outputs of the API

**In** is what the command takes; **Out** is what it gives back and where. Every command arrives on `APK.audio/Gui/Komands/TestSet/<Command>`.

### `get` — reads one value (10)

| Command | SCPI | In | Out | Group | |
|---|---|---|---|---|---|
| `Get_Idn` | `*IDN?` | — | CRD → `…/Reading/Get_Idn` | Common |  |
| `Get_Opc` | `*OPC?` | — | BOOL → `…/Reading/Get_Opc` | Common |  |
| `Get_Call_Status` | `CALL:STATUS?` | — | CRD → `…/Reading/Get_Call_Status` | CALL |  |
| `Get_Sinad` | `MEASure:AFANalyzer:SINAd?` | — | NR3 → `…/Reading/Get_Sinad` | MEASure |  |
| `Get_Audio_Level` | `MEASure:AUDio:LEVel?` | — | NR3 → `…/Reading/Get_Audio_Level` | MEASure |  |
| `Get_Thd` | `MEASure:AUDio:THD?` | — | NR3 → `…/Reading/Get_Thd` | MEASure |  |
| `Get_Ber` | `MEASure:BER?` | — | NR3 → `…/Reading/Get_Ber` | MEASure |  |
| `Get_Evm` | `MEASure:EVM?` | — | NR3 → `…/Reading/Get_Evm` | MEASure |  |
| `Get_Rf_Power` | `MEASure:RF:POWer?` | — | NR3 → `…/Reading/Get_Rf_Power` | MEASure |  |
| `Get_Audio_Freq` | `SOURce:AUDio:FREQuency?` | — | NR3 → `…/Reading/Get_Audio_Freq` | SOURce |  |

### `set` — writes one value (3)

| Command | SCPI | In | Out | Group | |
|---|---|---|---|---|---|
| `Set_Audio_Freq` | `SOURce:AUDio:FREQuency <value>` | `value` | — | SOURce |  |
| `Set_Audio_Level` | `SOURce:AUDio:LEVel <value>` | `value` | — | SOURce |  |
| `Set_Rf_Power` | `SOURce:RF:POWer <value>` | `value` | — | SOURce |  |

### `nab` — reads more than one thing (observation, telemetry) (10)

| Command | SCPI | In | Out | Group | |
|---|---|---|---|---|---|
| `Get_Idn` | `*IDN?` | — | CRD → `…/Reading/Get_Idn` | Common |  |
| `Get_Opc` | `*OPC?` | — | BOOL → `…/Reading/Get_Opc` | Common |  |
| `Get_Call_Status` | `CALL:STATUS?` | — | CRD → `…/Reading/Get_Call_Status` | CALL |  |
| `Get_Sinad` | `MEASure:AFANalyzer:SINAd?` | — | NR3 → `…/Reading/Get_Sinad` | MEASure |  |
| `Get_Audio_Level` | `MEASure:AUDio:LEVel?` | — | NR3 → `…/Reading/Get_Audio_Level` | MEASure |  |
| `Get_Thd` | `MEASure:AUDio:THD?` | — | NR3 → `…/Reading/Get_Thd` | MEASure |  |
| `Get_Ber` | `MEASure:BER?` | — | NR3 → `…/Reading/Get_Ber` | MEASure |  |
| `Get_Evm` | `MEASure:EVM?` | — | NR3 → `…/Reading/Get_Evm` | MEASure |  |
| `Get_Rf_Power` | `MEASure:RF:POWer?` | — | NR3 → `…/Reading/Get_Rf_Power` | MEASure |  |
| `Get_Audio_Freq` | `SOURce:AUDio:FREQuency?` | — | NR3 → `…/Reading/Get_Audio_Freq` | SOURce |  |

### `rig` — configures several arguments at once (1)

| Command | SCPI | In | Out | Group | |
|---|---|---|---|---|---|
| `Configure_Audio_Test` | `SOURce:AUDio:FREQuency <freq>;:SOURce:AUDio:LEVel <level>` | `freq`, `level` | — | SOURce |  |

### `do` — executes an action; takes no value (6)

| Command | SCPI | In | Out | Group | |
|---|---|---|---|---|---|
| `Clear_Status` | `*CLS` | — | — | Common |  |
| `Operation_Complete` | `*OPC` | — | — | Common |  |
| `Reset` | `*RST` | — | — | Common |  |
| `Wait_To_Continue` | `*WAI` | — | — | Common |  |
| `End_Call` | `CALL:END` | — | — | CALL |  |
| `Connect_Call` | `CALL:PCONnection` | — | — | CALL |  |
