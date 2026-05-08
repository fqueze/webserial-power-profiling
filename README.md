# WebSerial Power Profiling

Record power profiles directly in your browser using the
[Web Serial API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Serial_API),
without installing anything. Profiles can be opened in the
[Firefox Profiler](https://profiler.firefox.com).

This is the WebSerial counterpart of
[usb-power-profiling](https://github.com/fqueze/usb-power-profiling), which
required Node.js. Here, the page talks to the meter directly.

## Usage

Open `index.html` in a Web Serial-capable browser (Firefox 151+, or
Chromium-based browsers like Chrome and Edge — Safari doesn't support Web
Serial yet). Either open the file locally or host it on `https://` —
Web Serial is restricted to secure contexts.

1. Plug the power meter into the computer's USB port.
2. Click **Connect to a power meter…**.
3. Pick the meter's serial port in the chooser. By default the chooser only
   shows known-supported devices.
4. Sampling starts immediately. Use **Disconnect** to stop, **Reset samples**
   to clear and start a fresh recording, or the **profile** / **CSV** /
   **Open in the Firefox Profiler** links to export.

### Adding an unsupported device

Shift-click **Connect** to bypass the device filter — the chooser will then
show every serial port. This is the way to experiment with a new meter:
once you know which vendor/product id and protocol it uses, add an entry to
`SUPPORTED_DEVICES` near the top of the script in `index.html` and a driver
class alongside `YzxStudioDriver`.

## Supported devices

| Device | USB ids (vendor:product) | Driver |
|---|---|---|
| YZXStudio (e.g. 1280E) | `1a86:*` (CH340) | `YzxStudioDriver` |
| RuiDeng TC66C | `28e9:*` | `RuiDengDriver` |
| Shizuku (and rebrands, e.g. AVHzY CT-3 / Korona YK003C) | `0483:fffe`, `0483:ffff`, `0483:374b` | `ShizukuDriver` |

Other meters supported by the
[Node.js usb-power-profiling](https://github.com/fqueze/usb-power-profiling)
that use a USB-to-serial bridge can be ported the same way.
