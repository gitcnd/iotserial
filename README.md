# iotserial
Browser-based full-screen serial (RS232/TTL-Serial) console terminal for all IoT boards, with working DTR/RTS/Reset/GPIO0 control.  [Try Live](https://gitcnd.github.io/iotserial/xterm.html)

Serve this from any HTTPS:// website (browser-serial only works from secure origins) to get a local full-screen terminal to whatever serial-port-based device you plugged in to your machine.

This implementation includes the necessary DTR/RTS handling so it can work with every possible board out there (and allows users to do hardware-resets when that option is physically available)

NOTE: some boards use mutually exclusive\* flow control settings (e.g. and ESP32-cam won't work with DTR+RTS both set (holds it in reset forever) and others (e.g. S2-Mini) won't work with DTR+RTS both cleared (board impliments hardware flow control, so never sends because it thinks the other end is not ready...)

When linking to your page - the following options are available:

for boards which do not use flow control, the URL parameters "?rts=0&dtr=0&flow=0" can be passed in, and the javascript will adjust the port settings appropriately.

e.g. use this for ESP32-Cam or anything using an ESP programmer attachment (no flow control, uses RESET and GPIO wired to RTS and DTR pins etc) 

[https://gitcnd.github.io/xterm.html?rts=0&dtr=0&flow=0](https://gitcnd.github.io/xterm.html?rts=0&dtr=0&flow=0)

e.g. use this for "S2 Mini" (a board with flow control) or most boards with inbuilt USB-C:-

[https://gitcnd.github.io/xterm.html](https://gitcnd.github.io/xterm.html)


\* Boards using flow control need DTR and RTS to be set, so they know they can talk.
\* Boards NOT using flow control, need DTR and RTS to be cleared, because those are hooked up to the RESET and GPIO0 pins, and setting them locks up the MCU indefinitely (holds it in reset).

Paramaters:
* rts=0   makes the default state of the RTS pin to be clear (if this is missing, it defaults to being set to 1)
* dtr=0   makes the default state of the DTR pin to be clear (if this is missing, it defaults to being set to 1)
* flow=0  changes the wording on the buttons once connected (adds "RESET" and "GPIO" wording for chips not-using flow control)

this project contains static files imported from [https://github.com/xtermjs/xterm.js.git](https://github.com/xtermjs/xterm.js.git)
if you encounter terminal bugs, updating xterm.css, xterm.js, and xterm-addon-fit.js may address those.
