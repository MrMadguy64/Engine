# Engine
Universal DOS/Windows game engine.

Project aims at providing portable library to write universal DOS/Windows applications, including games. So it's similar to SDL or Allegro. But! The biggest difference - you don't even need to recompile your code to run it on other platform! Binaries themselves are portable! What it means? If your code works on Windows - it will also work on DOS. It's great feature for debugging. You can debug your code via using modern comfortable Windows tools, not obsoleted DOS ones. All extremely hard zero-debugging code writing is already done for you by me. Great? Yeah!

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

For now only VGA is supported. If you don't have extended memory - use SET DPMILDR=2 environment varaible.

Windows: Any Win32, including Windows 3.x + Win32s installed and Windows NT 3.x, Windows 9x/NT 4.x are recommended.

For now only GDI is supported.

**Modes supported:**

**DOS:**

HGC.drv
1) 720x348x50x1H, Flip is supported

VGA.drv
1) 160x100x70x4C, Flip is supported
2) 320x200x60x2C
3) 320x200x70x4E, Flip and TripleBufferFlip are supported
4) 640x200x60x1C
5) 640x200x70x4E, Flip and TripleBufferFlip are supported
6) 640x350x70x1, Flip is supported
7) 640x350x70x4E, Flip is supported
8) 640x480x60x1
9) 640x480x60x4E
10) 320x200x70x8
11) 320x200x70x8X, Flip and TripleBufferFlip are supported

For all modes: VSync is supported, Copy, Swap and TripleBufferSwap are supported

**Windows:**

GDI.drv
1) 1bpp
2) 2bpp, emulated
3) 4bpp
4) 8bpp
5) 15bpp
6) 16bpp
7) 24bpp
8) 32bpp

For all modes: VSync controls if WM_PAINT or direct rendering is performed, Copy and Swap are supported, NoDoubleBuffer is ignored

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
