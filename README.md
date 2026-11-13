# fMSX (MSX / MSX2) for ESP32 emulators

The MSX core of esp-box-emu: fMSX 6.0 by Marat Fayzullin ([fms.komkon.org/fMSX](https://fms.komkon.org/fMSX/)), with retro-go's `msxfix.c` wrapper (see `fmsx/README.md`).

## Layout

- `fmsx/`: the emulator core, as esp-box-emu has carried it (see below for its origin and changes).
- `port/`: the glue to the host firmware: `port/include/msx.hpp` is the API the
  firmware calls (init / run a frame / save / load / deinit, the video buffer for
  screenshots), `port/` implements it.

The port talks to the board through the `BoxEmu` singleton of
[esp-box-emu](https://github.com/esp-cpp/esp-box-emu) (`box-emu.hpp`: frame
buffers, `push_frame()`, `palette()`, `play_audio()`, `gamepad_state()`, ...).
[tab5-emu](https://github.com/esp-cpp/tab5-emu) provides the same API
(`using BoxEmu = Tab5Emu`), so the same sources build for both.

## Use

Add this repository as a submodule inside an ESP-IDF component and register its
sources from that component's `CMakeLists.txt` (each firmware keeps its own
component wrapper: the requirements, compile flags and linker fragment for
its target). See esp-box-emu's `components/msx/CMakeLists.txt`.

The history up to the split is esp-box-emu's history of `components/msx`.

## License

fMSX is copyright Marat Fayzullin and distributed under his own license: free for non-commercial use, see [fms.komkon.org/fMSX](https://fms.komkon.org/fMSX/) and the notices in `fmsx/src/`. It is not open source in the OSI sense; check its terms before redistributing.
