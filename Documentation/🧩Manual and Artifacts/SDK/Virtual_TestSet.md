# Virtual_TestSet — TestSet

← [SDK](../SDK.md)

**APK.audio** — APK.audio Virtual Test Set (Synthesized RF + Audio Multi-Function Emulator)

| | |
|---|---|
| Channels | 2 |
| HTTP | `:16303/api/instrument/TestSet/Virtual_TestSet` |
| `spec` | `/api/instrument/TestSet/Virtual_TestSet/Virtual_TestSet.api.json` |
| `health` | `/api/instrument/TestSet/Virtual_TestSet/health` |
| `get` | `/api/instrument/TestSet/Virtual_TestSet/get/<command>` |
| `set` | `/api/instrument/TestSet/Virtual_TestSet/set/<command>` |
| `nab` | `/api/instrument/TestSet/Virtual_TestSet/nab/<command>` |
| `rig` | `/api/instrument/TestSet/Virtual_TestSet/rig/<command>` |
| `do` | `/api/instrument/TestSet/Virtual_TestSet/do/<command>` |
| socket `ws` | `/ws/instrument/TestSet/Virtual_TestSet` |
| socket `readings` | `/ws/instrument/TestSet/Virtual_TestSet/readings` |
| socket `unix` | `/run/apk/instruments/TestSet.Virtual_TestSet.sock` |
| Domains | `rf_freq` 100000000…3000000000 Hz; `rf_power` -130…30 dBm; `audio_freq` 10…50000 Hz; `thd_n` 0.0001…100.0 %; `sinad` 0…120 dB |
| Reference | [commands tree](../../../Virtual_TestSet/commands_tree.md) · [sources](../../../Virtual_TestSet/SOURCES.md) |

## `get` — reads one value (10)

| Command | SCPI | Argument | Group | |
|---|---|---|---|---|
| `Get_Idn` | `*IDN?` |  | Common |  |
| `Get_Opc` | `*OPC?` |  | Common |  |
| `Get_Call_Status` | `CALL:STATUS?` |  | CALL |  |
| `Get_Sinad` | `MEASure:AFANalyzer:SINAd?` |  | MEASure |  |
| `Get_Audio_Level` | `MEASure:AUDio:LEVel?` |  | MEASure |  |
| `Get_Thd` | `MEASure:AUDio:THD?` |  | MEASure |  |
| `Get_Ber` | `MEASure:BER?` |  | MEASure |  |
| `Get_Evm` | `MEASure:EVM?` |  | MEASure |  |
| `Get_Rf_Power` | `MEASure:RF:POWer?` |  | MEASure |  |
| `Get_Audio_Freq` | `SOURce:AUDio:FREQuency?` |  | SOURce |  |

## `set` — writes one value (3)

| Command | SCPI | Argument | Group | |
|---|---|---|---|---|
| `Set_Audio_Freq` | `SOURce:AUDio:FREQuency <value>` | none | SOURce |  |
| `Set_Audio_Level` | `SOURce:AUDio:LEVel <value>` | none | SOURce |  |
| `Set_Rf_Power` | `SOURce:RF:POWer <value>` | none | SOURce |  |

## `nab` — reads more than one thing (observation, telemetry) (10)

| Command | SCPI | Argument | Group | |
|---|---|---|---|---|
| `Get_Idn` | `*IDN?` |  | Common |  |
| `Get_Opc` | `*OPC?` |  | Common |  |
| `Get_Call_Status` | `CALL:STATUS?` |  | CALL |  |
| `Get_Sinad` | `MEASure:AFANalyzer:SINAd?` |  | MEASure |  |
| `Get_Audio_Level` | `MEASure:AUDio:LEVel?` |  | MEASure |  |
| `Get_Thd` | `MEASure:AUDio:THD?` |  | MEASure |  |
| `Get_Ber` | `MEASure:BER?` |  | MEASure |  |
| `Get_Evm` | `MEASure:EVM?` |  | MEASure |  |
| `Get_Rf_Power` | `MEASure:RF:POWer?` |  | MEASure |  |
| `Get_Audio_Freq` | `SOURce:AUDio:FREQuency?` |  | SOURce |  |

## `rig` — configures several arguments at once (1)

| Command | SCPI | Argument | Group | |
|---|---|---|---|---|
| `Configure_Audio_Test` | `SOURce:AUDio:FREQuency <freq>;:SOURce:AUDio:LEVel <level>` | none | SOURce |  |

## `do` — executes an action; takes no value (6)

| Command | SCPI | Argument | Group | |
|---|---|---|---|---|
| `Clear_Status` | `*CLS` |  | Common |  |
| `Operation_Complete` | `*OPC` |  | Common |  |
| `Reset` | `*RST` |  | Common |  |
| `Wait_To_Continue` | `*WAI` |  | Common |  |
| `End_Call` | `CALL:END` |  | CALL |  |
| `Connect_Call` | `CALL:PCONnection` |  | CALL |  |
