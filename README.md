# Tensiometer display

A one-page Web Bluetooth client for the tensiometer strain-gauge node. Open it in Chrome on
Android (or desktop Chrome with a Bluetooth adapter), tap **Connect**, pick the gauge, and the
force shows in kgf in large digits at the gauge's notification rate (about 10 Hz), next to a
vertical bar from 0 % to 120 % of the selected Tost weak link (Blue 600, Red 750, Brown 850 daN;
the selection is remembered). Above 100 % the bar turns red. Tap the number for full screen. The
page keeps the screen awake and reconnects on its own if the link drops.

Hosted on GitHub Pages: https://ivan-galinskiy.github.io/tensiometer-display/

A URL fragment narrows the device picker to one name: `#RX` offers only `Tension RX`, the receiver
in the glider (`#gauge` would offer `Tension gauge`). The receiver shows this link as a QR code when
its BOOT button is pressed.

The gauge's GATT, defined in the firmware of the (private) `tensiometer` repository:

| item | value |
|---|---|
| service | Industrial Measurement Device, `0x185A` |
| characteristic | Force, `0x2C07`, read + notify |
| format | `sint32` little-endian, exponent -3, newton (millinewtons) |
| time | Current Time service `0x1805`, Current Time `0x2A2B`, write: the page writes the time in UTC on every connect, setting the device's log clock: the phone's clock, corrected by the `Date` header of a request to this site when it is more than 2 s off |

Web Bluetooth needs a secure context, which is why the page lives on Pages rather than being
opened from a file.
