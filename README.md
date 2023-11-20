# Engine
Universal DOS/Windows game engine.

Project aims at providing portable library to write universal DOS/Windows application, including games. So it's similar to SDL or Allegro. But! The biggest difference - you don't even need to recompile your code to run it on other platform! Binaries themselves are portable! What it means? If your code works on Windows - it will also work on DOS. It's great feature for debugging. You can debug your code via using modern comfortable Windows tools, not obsoleted DOS ones. All extremely hard zero-debugging code writing is already done for you by me. Great? Yeah!

**License:**

Engine can be used for free for personal non-commercial purpose only. Any purpose, that involves explicit or implicit revenue, including indirect one (in case of budget or government organizations, educational purposes, etc.) - is allowed only after buying commercial license.

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

DOS:
1) VGA 320x200x70x4E, VSync is supported, NoDoubleBuffer, Flip, Copy and Swap are supported
2) VGA 640x200x70x4E, VSync is supported, NoDoubleBuffer, Flip, Copy and Swap are supported
3) VGA 640x350x70x4E, VSync is supported, NoDoubleBuffer, Flip and Copy are supported
4) VGA 640x480x60x4E, VSync is supported, NoDoubleBuffer is supported
5) VGA 320x200x70x8, VSync is supported, NoDoubleBuffer, Copy and Swap are supported
6) VGA 320x200x70x8X, VSync is supported, NoDoubleBuffer, Flip, Copy and Swap are suppoted

Windows:
1) GDI 8bit only, VSync controls if WM_PAINT or direct rendering is performed, Copy and Swap are supported, NoDoubleBuffer is ignored

**OS support:**

Global settings:

1) Enable/disable mouse option allows switching mouse handling off to prevent unnecessary performance penalty

DOS:

1) Timer settings: RTC or PIT, more precision - bigger perofrmance penalty

Windows 3.x/NT 3.x:

No options available for now

Windows 9x/NT 4.x:

1) Async timer for smoother controls, but can slow game down
2) Async rendering for smoother FPS
3) Switching both off essentially turns driver into Windows 3.x+Win32s/NT 3.x one
4) Priorities allow better tuning for single-core CPU scenario
