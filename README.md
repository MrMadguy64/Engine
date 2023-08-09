# Engine
Universal DOS/Windows game engine

**License:**

Engine can be used for free for personal non-commercial purpose only. Any purpose, that involves explicit or implicit revenue, including indirect one (in case of budget or government organizations, educational purposes, etc.) - is allowed only after buying commercial license.

**License philosophy:**

Programmers should be professionals, not just enthusiasts, who have to provide unrelated services in order to earn money. If one uses my work to earn money - then he should share part of his revenue with me. If you earn money via clogging nails, then why do you think hammer should be free for you? Buy it! I've put my effort into making tool for you to earn money. And it's like law of energy conservation. Every drop of sweat should pay off.

**Please note!** If you want to launch game's exe directly - then copy Data directory to exe's directory.

**System requirements:**

DOS: Same as for HX, i386, DOS 5.0
For now only VGA is supported. If you don't have extended memory - use SET DPMILDR=2 environment varaible.

Windows: Any Win32, including Windows 3.x + Win32s installed and Windows NT 3.x, Windows 9x/NT 4.x are recommended.
For now only GDI is supported.

**Modes supported:**

DOS:
1) VGA 320x200x70x8, VSync supported, Copy and Swap supported
2) VGA 320x200x70x8X, VSync supported, Flip, Copy and Swap suppoted

Windows:
1) GDI 8bit only, VSync controls if WM_PAINT or direct rendering is performed, Copy and Swap are supported

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
