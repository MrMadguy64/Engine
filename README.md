# Engine
Universal DOS/Windows game engine.

Project aims at providing portable library to write universal DOS/Windows applications, including games. So it's similar to SDL or Allegro. But! The biggest difference - you don't even need to recompile your code to run it on other platform! Binaries themselves are portable! What it means? If your code works on Windows - it will also work on DOS. It's great feature for debugging. You can debug your code via using modern comfortable Windows tools, not obsoleted DOS ones. All extremely hard zero-debugging code writing is already done for you by me. Great? Yeah!

**Demos:**

[Game Engine Tetris Demo](https://github.com/MrMadguy64/EngineTetrisDemo)

[Game Engine BmpView Demo](https://github.com/MrMadguy64/EngineBmpViewDemo)

**License:**

Software can be used for free for personal non-commercial purpose only. Any purpose, that involves explicit or implicit revenue, including indirect one (in case of budget or government organizations, educational purposes, etc.) - is allowed only after buying commercial license.

Any form of reverse-engineering is forbidden, including but not limited to debugging, decompiling, disassembling.

**License philosophy:**

Programmers should be professionals, not just enthusiasts, who have to provide unrelated services in order to earn money. If one uses my work to earn money - then he should share part of his revenue with me. If you earn money via clogging nails, then why do you think hammer should be free for you? Buy it! I've put my effort into making tool for you to earn money. And it's like law of energy conservation. Every drop of sweat should pay off.

**Warranty disclaimer:** 

You use this software at your own risk. It's provided "as is" without any express or implied warranty of any kind, including warranties of merchantability or fitness for any particular purpose. Author isn't liable for any direct, indirect, incidental, special, exemplary, or consequential damage, caused by using this software.

**Please note!** If you want to launch game's exe directly - then copy Data directory to exe's directory.

**System requirements:**

DOS: Same as for HX, i386, DOS 5.0.

If you don't have extended memory - use SET DPMILDR=2 environment varaible.

Windows: Any Win32, including Windows 3.x + Win32s installed and Windows NT 3.x, Windows 9x/NT 4.x are recommended.

For now only GDI is supported.

**Warning!** Since SP4 WinNT 3.51 has bug: some sort of race condition while initializing Kernel32.dll. Game.exe crashes with error 0xc000142 in Kernel32.dll.

Possible workarounds:
1) Don't use Launcher.exe. Copy Data directory to Bin32 and launch Game.exe directly.
2) Try to change command line length via adding arbitrary string to it's end.

**Modes supported:**

**DOS:**

For all modes: VSync, NoDoubleBuffer, Copy, Swap and TripleBufferSwap are supported

**Please note!**: Dynamic - mode, for which mode info is calculated on fly. If mode matches standard one - it's unmodified and marked as Standard. All modes support VSync, but Flip and TripleBufferFlip support can be specific to every mode. If there are duplicate modes, like 320x200x70x8 and 320x200x70x8X, that both can be picked via demanding unmodified 8bpp format - first one always has priority. Second one is picked only if first one is filtered out by some other parameters. So 1bpp CGA mode can only be choosen via specifying 1C format explicity. Only "fullsceen" modes are supported. While any mode down to 8x1 is actually possible, if mode timings don't match standard ones - only part of screen is occupied, that is pointless feature.

HGC.drv
1) 720x348x50x1H, Flip is supported

EGA.drv
1) 1, Dynamic, 320x200..640x350
2) 640x200x60x1C
3) 320x200x60x2C
4) 4E, Dynamic, 320x200..640x350
5) 4T, Dynamic, 80x25..160x350, if enough video memory

Horizontal resolutions 320 and 640 are supported with divisors 1, 2, 4. Vertical resoutions 200 and 350 are supported with divisors 1..14 for EGA/MDA and 1..8 for CGA (up to 32 can be supported, but it's pointless, plus EGA/CGA/MDA font has 14/8/14 pixels height). Values are rounded up to closest integers.

VGA.drv
1) 1, Dynamic, 160x22..720x480
2) 640x200x70x1C
3) 320x200x70x2C
4) 4V, Dynamic, 160x22..720x480
5) 4E, Dynamic, 160x22..720x480
6) 4T, Dynamic, 80x22..180x480, if enough video memory
7) 8, Dynamic, 160x22..360x480, if enough video memory
8) 8X, Dynamic, 160x22..360x480

Horizontal resolutions 320, 640, 360, 720 are supported with divisors 1, 2, 4. Vertical resoutions 350, 400, 480 are supported with divisors 1..16 (up to 32 can be supported, but it's pointless, plus VGA font has 16 pixels height). Values are rounded up to closest integers. Don't forget to set Compatiblity to Experimental for 360/720 modes!

**Windows:**

For all modes: VSync controls if WM_PAINT or direct rendering is performed, Copy and Swap are supported, NoDoubleBuffer is ignored

GDI.drv
1) 1bpp
2) 2bpp, emulated
3) 4bpp
4) 8bpp
5) 15bpp
6) 16bpp
7) 24bpp
8) 32bpp

**Please note!** Format support depends on specific driver implementation and currently selected video mode. You'll get blank screen, if format is unsupported, garbled colors or distorted image, if it's supported partially. Testing has shown, that some drivers can even support undocumented formats. They aren't implemented in GDI driver now. I'm not sure, if they should be implemented. And if yes - then how they should be implemented, because they're purely GDI specific.

**Please note!** Emulated mode if unsupported by GDI, requires software processing and therefore can be ~2x slower.

**OS support:**

Global settings:

1) Enable/disable mouse option allows switching mouse handling off to prevent unnecessary performance penalty

DOS:

1) Timer settings: RTC or PIT, more precision - bigger perofrmance penalty
2) Mouse settings: use normal mouse handling or alternative

Windows 3.x/NT 3.x:

No options available for now

Windows 9x/NT 4.x:

1) Async timer for smoother controls, but can slow game down
2) Async rendering for smoother FPS
3) Switching both off essentially turns driver into Windows 3.x+Win32s/NT 3.x one
4) Priorities allow better tuning for single-core CPU scenario

All systems:

1) Video driver setting
