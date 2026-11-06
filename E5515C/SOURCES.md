# Sources — Agilent 8960 / E5515C / E5515E

Agilent 8960 Series 10 Wireless Communications Test Set.

## Manuals & References

* Keysight 8960 (E5515C/E) Online User Guides: <https://www.keysight.com/us/en/library/manuals/user-manual/8960-e5515ce-online-user-guides-607243.html>
* Keysight 8960 Comprehensive Documentation Guide (PDF 9018-01190): <https://www.keysight.com/tj/en/assets/9018-01190/user-manuals/9018-01190.pdf>
* Keysight 8960 Quick Test Software Help: <https://www.keysight.com/us/en/lib/resources/help-files/8960-quick-test-software-2408985.html>

## Core Subsystems
* `CALL`: Cellular Call Processing, protocol state machine, band/channel, RF power, and speech loopback
* `AFANalyzer`: Audio frequency, RMS AC/DC voltage, THD / THD+N distortion, and SINAD
* `MEASure`: Parametric RF measurements (Tx Power, EVM, BER, FER, OBW, Frequency Error)
* `SYSTem`: Error queue, display update / screen blanking for GPIB speed optimization

## Trace — no trace query declared yet (ROAD-3559, 2026-11-05)

The recorder traces a box whose library declares a trace-data query and its
frequency start/stop (CAPTURE.Recorder `askers/sweep.rs`). This family declares
neither, on purpose, until the manual answers three things it has not yet:

* **The query.** Keysight's 8960 lab-application references describe a Spectrum
  Monitor: `FETCh:SMONitor:TRACe?` "returns Integrity Indicator followed by 401
  points representing the amplitude results (in dBm) of the trace data", the
  points lying "within the current span, relative to the center frequency"
  (<https://helpfiles.keysight.com/csg/wcdma/wcdma_hpib_fetch_smonitor.html>),
  span set and queried by `SETup:SMONitor:FREQuency:SPAN` (125 kHz to 100 MHz,
  <https://helpfiles.keysight.com/csg/wcdma/wcdma_hpib_setup_smonitor.html>).
  Those pages are the WCDMA lab application's, not this unit's installed one,
  and name no product; the GSM pages found are the E6601A's.
* **The centre.** Neither page names the query for the frequency the 401 points
  are relative to, so no start/stop can be computed. (On the E6601A it is
  `CALCulate:SMONitor:SCALe:FREQuency:MCENter` — a different instrument.)
* **Who starts it.** Results exist only after `INITiate:SMONitor`, which the
  recorder must never send (it only reads). Reading a measurement somebody else
  started is a decision, not a lookup.

Add the queries to `E5515C.komand` (8960 and E5515E inherit) only from this
unit's installed application's reference, with its centre query; the recorder
then also needs to skip the leading integrity indicator.
