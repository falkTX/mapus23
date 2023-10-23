# MOD Audio Presentation for Ubuntu Summit 2023

NOTICE: work in progress rough sketch

target: 50 minutes

## Pre-presentation

- [ ] Ensure macbook linux system can use external screen via HDMI
- [ ] Ensure Dwarf network connection
- [ ] Check if Dwarf usb audio is usable
- [ ] Check high-dpi, with libreoffice presentation stuff and dpf+imgui (in case that gets done in time?)
- [ ] Prepare photo of the Dwarf front-faced with HMI screen on
- [ ] Prepare photo of the Dwarf back-side for easy IO description
- [ ] Prepare photo of the Dwarf internals (or have unit open?)
- [ ] Prepare basic graph/node sketch of Dwarf/Linux (dns server) -> USB (network device) -> PC
- [ ] Prepare Dwarf pedalboard useful for initial demo purposes
- [ ] Prepare photo of Duo marsboard adapter
- [ ] Prepare xrun/latency-spike demo with memset tool (stop RT/big services, run rt-tests, run memset)
- [ ] Check usability of mod-screenshot tool
- [ ] Calculate time estimates

## Intro

0. Boot up MOD Dwarf (or have it already plugged in)
1. Brief explanation about what the Dwarf is
2. Connect to PC, open web gui with demo pedalboard, briefly explain workflow
3. List the topics of the talk

- architecture/design decisions
- iterations
- lessons learned

## Choosing a base SoM

0. "Preface": why ARM vs others
1. Define requirements first
2. SoM socketable model, non-standard socket but still doable to iterate, potentially soldered model (not during initial development)
3. many components unused, but expected with these SoMs
...

## Initial experiments and testing

1. Start with a dev board, regular Linux images
2. Check performance and stability (LESSONS LEARNED: make sure usb driver is good!!)
3. Initial tests with RT audio (bless be mainline kernel with many RT things)
4. Investigate deploy methods (LESSONS LEARNED: make sure to understand from-scratch deploy methods!!)

## Getting hands dirty (wait...)

A few critical things to solve first

1. The versioning problem (how to ensure consistency of what the user is running)
2. How to deal with updates? (would contain the entire "OS")
3. Reproducible builds? (LESSONS LEARNED: use containers to ensure everyone has the same setup, saves time long-term)
4. Factory-reset? (needs to be exposed to users too)

Let's go custom builds, we chose buildroot as helper at the time (2016)

## Booting up: Initial steps

1. Manual build of bootloader, partitioning and other hw specific (lets get it booting something)
2. Getting a kernel to build and run, quick setup using vendor kernel if needed
3. Add busybox and other tools, ensure (some) hw works as expected (RAM test, eMMC)
4. Set up dns server (dnsmasqd), ssh server, get usb network for quick develop iterations
5. Start tweaking kernel, mainline even if doable, and get all details up to speed

## Partitioning and restore

1. Define partitions (restore, system, user-data)
2. Create kernel variant for handling updates/restore (disable RT and audio)
3. Entire restore filesystem embed in kernel image, boots in RAM (so entire disk can be safely erased if necessary)

## Handling updates

Likely nowadays automated with some other tools?

1. Define install/update image (tar for each partition content)
2. Define update process (format partition, extract tar, feedback through LEDs)
3. Generate the entire thing in 1 go
4. Have a way to do initial flash matching generated build (with only restore mode)

Hurray, a deployable device!

(note to audience: some of the previous and future points would be done in parallel)

## Audio setup

- JACK server on top of ALSA (cs4565 I2S device)
- setup mod-host and mod-ui
- introduce ttymidi, midi-merger, audio-bridge

## Human-Machine Interface

- basic mod-controller details
- top-board and bottom-board
- give uart access, can now run custom commands (like reboot)
- hook into bootloader for manually entering restore mode (also maskrom for rockchip)

## Self-test and QC

1. how to test all hw features work? introducing self-test mode
2. audio loopback, midi loopback, usb host to device
3. test of hw buttons, knobs, leds, screen
4. all units must pass self-test at least once

## System tweaks and fine-tuning

- JACK with internal clients
- JACK with private futexes
... ? TODO more stuff here
- IRQ tuning
- nightmares of hw quirks (quick demo of memset issue, mention USB driver)
- throwing cpu at the noise problem

## The internet side of things

- Cloud builds (show slack bot? internet access even good enough for it?)
- Cloud side for OS releases
- Plugin store

Note: device does not connect to the internet, web browser does and sends data to Dwarf webserver

## Little extra cloud things

- Pedalboard sharing
- Plugin builder

## Conclusion

lots of work, but we end up with:

- deploy and usage as easy as possible
- consistent OS versions
- device-specific tuning for the best performance possible
- automated builds and updates (*assuming integration with cloud side)
