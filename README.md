# MOD Audio Presentation for Ubuntu Summit 2023

Target: 50 minutes

- Presentation title
- About me
- Quick Dwarf intro
- Presentation body
- Cloud-related demos depending on time
- Conclusion
- Questions

## Pre-presentation

- [x] Ensure macbook linux system can use external screen via HDMI
- [x] Ensure Dwarf network connection
- [ ] Check if Dwarf usb audio is usable
- [ ] Check high-dpi, with libreoffice presentation stuff
- [x] Prepare photo of the Dwarf front-faced with HMI screen on
- [x] Prepare photo of the Dwarf internals (or have unit open?)
- [ ] Prepare basic graph/node sketch of Dwarf/Linux (dns server) -> USB (network device) -> PC
- [ ] Prepare Dwarf pedalboard useful for initial demo purposes
- [ ] Prepare xrun/latency-spike demo with memset tool (stop RT/big services, run rt-tests, run memset)
- [ ] macbook setup of Dwarf kernel build, for live-demo push
- [ ] Calculate time estimates

TODO fit in there somewhere:
- "The versioning problem" as its single topic? (TBD)

## Demos

Stuff that needs separate showcasing:

- MPB kernel menuconfig, dirclean, rebuild, publish
- kernel tweaks quick deploy
- update image tar
- enter restore mode, do manual update
- force host crash, reload and recover
- hmi bootloader restore, markrom ??
- license api
- self-test mode
- mod-memset
- mod-noise-removal

## LICENSE

CC0 1.0 Universal, see [LICENSE](LICENSE)

LICENSE applies only to this `README.md` and the `pres.odp` text, artwork is copyright MOD Audio UG and used with permission.
