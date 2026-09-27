# Tensiometer display

A one-page Web Bluetooth client for the tensiometer strain-gauge node. Open it in Chrome on
Android (or desktop Chrome with a Bluetooth adapter), tap **Connect**, pick the gauge, and the
force shows in large digits at the gauge's notification rate (about 10 Hz). Tap the number for
full screen. The page keeps the screen awake and reconnects on its own if the link drops.

Hosted on GitHub Pages: https://ivan-galinskiy.github.io/tensiometer-display/

The gauge's GATT, defined in the firmware of the (private) `tensiometer` repository:

| item | value |
|---|---|
| service | Industrial Measurement Device, `0x185A` |
| characteristic | Force, `0x2C07`, read + notify |
| format | `sint32` little-endian, exponent -3, newton (millinewtons) |

Web Bluetooth needs a secure context, which is why the page lives on Pages rather than being
opened from a file.
