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

Programmers should be professionals, not just enthusiasts, who have to provide unrelated services in order to earn money. If one uses my work to earn money - then he should share part of his revenue with me. If you earn money via clogging nails, then why do you think hammer should be free for you? Buy it! I've put my effort into making tool for you to earn money. And it's like law of energy conservation. Every drop of sweat should pay off. It's not fair, if some tool is used to earn billions of dollars, while it's author should be enthusiast, who can count on sporadic donations only. This includes new threat - AI. For now it isn't well regulated. Free projects can be used for AI training, that can be treated as commercial educational purposes, as goal of such training - is to earn profits then, while devaluing initial author's effort.

**Warranty disclaimer:** 

You use this software at your own risk. It's provided "as is" without any express or implied warranty of any kind, including warranties of merchantability or fitness for any particular purpose. Author isn't liable for any direct, indirect, incidental, special, exemplary, or consequential damage, caused by using this software.

**Please note!** If you want to launch game's exe directly - then copy Data directory to exe's directory. Please remember, that Game.exe doesn't contain HX stub! You should install HXLDR32.EXE as TSR before trying to run Game.exe.

**System requirements:**

DOS: Same as for HX, i386, DOS 5.0.

If you don't have extended memory - use SET DPMILDR=2 environment varaible.

**Warning!** If you want to complie your application as GUI one, you need modified version of DPMILD32.exe - one compiled with ?NOGUIAPPS=0 and ?ALLOWGUIAPPS=0 options.

Windows: Any Win32, including Windows 3.x + Win32s installed and Windows NT 3.x, Windows 9x/NT 4.x are recommended.

For now only GDI is supported.

**Warning!** Since SP4 WinNT 3.51 has bug: some sort of race condition while initializing Kernel32.dll. Game.exe crashes with error 0xc000142 in Kernel32.dll.

Possible workarounds:
1) Don't use Launcher.exe. Copy Data directory to Bin32 and launch Game.exe directly.
2) Try to change command line length via adding arbitrary string to it's end.

**Game.exe controls:**

1) Arrow keys - move bitmap.
2) WASD - move bitmap mask.
3) R - reset bitmap mask.
4) B - toggle text background: transparent, extent (red), width (blue).
5) Mouse - cursor and mouse buttons state.

**Global options:**

Mode filtering:

First matching mode is picked. Mode conflicts can possibly happen, when modes are listed by external routines (like in case of SVGA). But video driver should have extra options to solve such conflics.

1) Width, pixels, 0 - unspecified, any value match
2) Height, pixels, 0 - unspecified, any value match
3) Frequency, Hz, 0 - unspecified, any value match
4) Pixel format, exact value matched first, meta format matched then. Meta formats make life easier. They allow matching bpp only, i.e. picking video-card specific modes like 4bppV or 4bppE via simply specifying 4bpp. Please note. While some drivers allow some sort of "better modes lised first" priority, others don't, like SVGA one for example.
5) Compatibility. Safety measure, that filters out modes, that can be potentially dangerous to use. Set higher values at your own risk! Set lower values, if you have problems.

Mode options:

7) VSync, exact value, fails if unsupported
8) SwapEffect, exact value, fails if unsupported. Flip must be supported by hardware. In all other cases support depends on amount of video and system memory availiable. Falls back to SM variants, if not enough video memory available. There are just two possible cases from game's point of view: copy and flip. Game's rendering behavior is different depending on which one is chosen. It recommended to support both.
9) Buffering, falls back to corresponding lower value, if unsupported. Used in modes, where direct rendering to video buffer can cause glitches or can even be unsupported. Overall logic - higer value = better quality, but slower rendering. As swap effect is transparent for video driver (i.e. swap effects aren't hardcoded), it can't determine, if some buffering mode is more effective than other. It's up to user to do it. Buffered variants are only available, if video card has enough video memory.

**Modes supported:**

**DOS:**

For all modes: VSync, NoDoubleBuffer, Copy, Swap, TripleBufferSwap, SMCopy, SMSwap and SMTripleBufferSwap are supported, if opposite isn't stated explicitly.

**Please note!**: Dynamic - mode, for which mode info is calculated on fly. If mode matches standard one - it's unmodified and marked as Standard. All modes support VSync, but Flip and TripleBufferFlip support can be specific to every mode. If there are duplicate modes, like 320x200x70x8 and 320x200x70x8X, that both can be picked via demanding unmodified 8bpp format - first one always has priority. Second one is picked only if first one is filtered out by some other parameters. So 1bpp CGA mode can only be choosen via specifying 1C format explicity. Only "fullsceen" modes are supported. While any mode down to 8x1 is actually possible, if mode timings don't match standard ones - only part of screen is occupied, that is pointless feature.

**Dual display support:** Engine can't render to both adapters at the same time now. But dual display setup is supported to some degree. Adapter is detected, no matter if it's active or not. But it most likely wouldn't operate properly, if it wouldn't be made active. Enigne itself doesn't do it now. So for now it's recommended to make adapter active manually before starting any application, that uses Engine.

MDA.drv
1) 160x25x50x1M
2) 160x25x50xMM

VSync is unsupported.

HGC.drv
1) 160x25x50x1M
2) 160x25x50xMM
3) 720x348x50x1H, Flip is supported

Use ModeConfig option to control, whether half or full mode is used. Full mode can't be used, if color video card is installed due to memory address conflict. Following modes are supported:
1) Detect. Use half mode, if color video card is present, use full otherwise.
2) Force half mode. Use, if color video card isn't autodetected correctly.
3) Force full mode. Use, if no other video card is present or if it doesn't work in text mode.

CGA.drv
1) 640x200x60x1C
2) 320x200x60x1C
3) 4T, Dynamic, 80x25..160x100

Horizontal resolutions 320 and 640 are supported with divisor 4. Vertial resolution 200 is supported with divisors 2..8. Values are rounded down to closest integers. Please note: only 2, 4 and 8 divisors use Standard timings - others require Compatiblity to be set to Experimental!

EGA.drv
1) 1P, Dynamic, 320x6..640x350
2) 640x200x60x1C
3) 1T, Dynamic, 80x6..160x350, if enough video memory
4) MP, Dynamic, 320x6..640x350 (EGA/CGA only)
5) ME, Dynamic, 320x6..640x350 (EGA/CGA only)
6) 640x350x60xME (MDA only)
7) 160x25x60xMM (MDA only)
8) MT, Dynamic, 80x6..160x350, if enough video memory
9) 2P, Dynamic, 320x6..640x350
10) 2E, Dynamic, 320x6..640x350
11) 320x200x60x2C
12) 2T, Dynamic, 80x6..160x350, if enough video memory
13) 4E, Dynamic, 320x6..640x350
14) 4T, Dynamic, 80x6..160x350, if enough video memory

Horizontal resolutions 320 and 640 are supported with divisors 1, 2, 4. Vertial resolutions 200 and 350 with divisors 1..32 in EGA graphic modes, 200 with divisors 1..32 in CGA graphic modes, only 350 in MDA graphic modes, 200 and 350 with divisors 1..14/31 in EGA text modes, 200 with divisors 1..8/31 for CGA in text modes and only 1 for MDA in text modes (depends on CharGenLoadMode setting: enabled - 31, disabled - 14/8, depends on HeightRoundMode). Limited to 31 in text modes due to underline. Only way to hide it - to set it's position to 32. Thus fonts can't have 32 rows. Only 31.

CharGenLoadMode option:
1) Enabled only if necessary (>8/14 lines)
2) Force enabled (even for standard modes) - use in case of problems with default character generator
3) Force disabled (disables modes, that require it) - use in case of compatibility problems with character generator load code

HeightRoundMode option:
1) Round up, preserves vertical resolution, but last line may be cut
2) Round down, vertical resolution may decrease, but all lines have the same height

Different amounts of video memory are supported. Amount of memory installed doesn't affect text modes, as all text modes require 64Kb only. For graphic modes amount of memory affects number of pages avilialbe. Modes, that require more than 64Kb VRAM (640x350 for example) are special case. If video card has only 64Kb VRAM installed - these modes can be 2bpp only (1, ME, 2E).

VGA.drv
1) 1P, Dynamic, 160x5..720x480
2) 1C, Dynamic, 320x200..720x480, if enough video memory
3) 1T, Dynamic, 80x5..180x480, if enough video memory
4) MP, Dynamic, 80x5..180x480, if enough video memory
5) MV, Dynamic, 320x5..720x480
6) ME, Dynamic, 320x5..720x480
7) MM, Dynamic, 80x5..180x480, if enough video memory (Mono only)
8) MT, Dynamic, 80x5..180x480, if enough video memory
9) 2P, Dynamic, 80x5..180x480, if enough video memory
10) 2V, Dynamic, 320x5..720x480
11) 2E, Dynamic, 320x5..720x480
12) 2C, Dynamic, 320x200..720x480, if enough video memory
13) 2T, Dynamic, 80x5..180x480, if enough video memory
14) 4V, Dynamic, 320x5..720x480
15) 4E, Dynamic, 320x5..720x480
16) 4T, Dynamic, 80x5..180x480, if enough video memory
17) 4P, Dynamic, 320x5..720x480, if enough video memory
18) 8P, Dynamic, 160x5..360x480, if enough video memory
19) 8X, Dynamic, 160x5..360x480
20) 8D, Dynamic, 160x5..360x480, if enough video memory
21) 8R, Dynamic, 160x5..360x480, if enough video memory
22) 8XD, Dynamic, 160x5..360x480
23) 8XR, Dynamic, 160x5..360x480    

Horizontal resolutions 320, 640, 360, 720 are supported with divisors 1, 2, 4. Vertical resoutions 350, 400, 480 are supported with divisors 1..64 (even values only, if >32) in graphic modes and 1..8/14/16/62 in text modes (depends on CharGenLoadMode setting: enabled - 62, disabled - 8/14/16, depends on CharGenFontMode/CharGenMonoMode, depends on HeightRoundMode). Limited to 31 in text modes due to underline. Only way to hide it - to set it's position to 32. Thus fonts can't have 32 rows. Only 31. ScanLineDouble bit, that is used by CRTC for CGA emulation, can double this value. Thus, max divisor is 62 in text modes. Don't forget to set Compatiblity to Experimental for 360/720 modes!

CGA and HGC modes are special case. Only divisor 2 is available for both horizontal and vertical resolutions. Vertcal resolution is limited by three factors: max bank size, max number of banks, max number of lines per bank. Max bank size is always 8Kb. For CGA max number of banks is 2, for HGC - is 4. If CGALineLimit mode is enabled, only 128 lines per bank are avalable. Vertial resolution is affected by HeightRoundMode. If HeightRoundMode is round down, then Height = Height - (Height mod Banks).

CharGenLoadMode option:
1) Enabled only if necessary (>8/14/16 lines)
2) Force enabled (even for standard modes) - use in case of problems with default character generator
3) Force disabled (disables modes, that require it) - use in case of compatibility problems with character generator load code

HeightRoundMode option:
1) Round up, preserves vertical resolution, but last line may be cut
2) Round down, vertical resolution may decrease, but all lines have the same height

CGAAllow64Kb option:
1) Disabled - 32Kb VRAM, compatible with standard CGA modes
2) Enabled - 64Kb VRAM, doesn't affect list of available resolutions - only number of pages available

CGALineLimit option:
1) Enabled - 128 lines per bank max, compatible with standard CGA modes
2) Disabled - not limited, any number, that would fit into 8Kb bank, allows some modes, like CGA 320x400 1bpp (200 lines per bank)

CharGenFontMode option:
Controls, what text modes are considered to be base stanard ones to be modified. It's important, because this setting affects CharGenLoadMode and Compatibility settings. Choosing wrong settign may cause garbled picture or wrong mode selection. Certain font height can be: assumed, forced, detected. Unless you'd change font height purposely, it's safe to assume it to be 8x16 to avoid unnecessary API calls. VGA info only detection method is unreliable on IBM VGA, because IBM VGA uses 8x8 font bit only as temporary storage when color->mono mode switching. It's value can be lost in case of mono->color mode switch. It's unused, if secondary adapter is present, as color<->mono mode switches are impossible in this case. It's reliable in single adapter mode only and only if color modes are used. But it can be reliable in later BIOSes and emulators, that assume wrongly documented behavior. 

CharGenMonoMode option:
IBM VGA-specific option. IBM VGA has very specific behavior, when performing color<->mono switches. 8x14 font is forced in mono modes, if 8x16 font isn't choosen. Problem is - video card can be in color mode, when font height is detected via CharGenFontMode. Therefore we should fall back to 8x14, if 8x8 is selected or detected, but mode selected is mono one. Later BIOSes may allow 8x8 in mono modes. Especially emulators. Simply because this behavior isn't documented well enough.

CharGenRestoreMode:
Font height is global settings. It isn't restored automatically, that can cause other programs to operate wrongly. Use this setting to control, how font height setting is restored, when VGA driver is uninited. You can: do nothing, force certain height, restore previously detected value. Unless you'd change font height purposely, it's better to use "Don't restore" option in order to avoid unnecessary API calls.

Mono monitor support doesn't require any special actions - it's supported by BIOS internally.

Mono modes are handled differently. There are 3 possible variants:
1) Single - all modes listed above are supported, Mx modes are emulated due to collision between color and mono implementations.
2) Dual color - Mx modes are emulated, MM modes are unsupported.
3) Dual mono - only Mx and MM modes are supported.

SVGA

Following options are common for all SVGA drivers:

If no direct color info is provided by BIOS, following options can be useful:
1) Force15bpp: Non-standard modes only. Some old BIOSes may support 15bpp modes only, but report them as 16bpp. For example VBE 1.2 standard states, that VBE 1.0-1.1 BIOSes do it. Set this option to Enabled in this case.
2) Force32bpp: Standard modes only. Standard VESA modes should be 24bpp, as stated in VBE standard. But some old video cards may support 32bpp instead. Set this option to Enabled in this case. As scanline lenght is most like different for 24bpp and 32bpp modes, Guess option can be used to try to guess supported format.
3) ForceBGR: Both standard and non-standard modes. Even rarer case. Not sure, if such video cards exist. Video card supports BGR formats instead of RGB. Set this option to Enabled in this case.

Compatibility options:
1) DisableVGAIO: Disable features, that require direct access to VGA IO ports - planar modes, VSync.
2) DisableVGABIOS: Disable features, that require VGA BIOS calls - set palette, set blink in text modes.
3) DisableVGATTY: Disable features, that require VGA TTY calls - hide cursor in text modes.
4) DisableDirectBankSwitch: Don't use bank switch procedure, provided by 4F01h - force BIOS calls.
6) PagesAvailable: 0 is default - it's the best option. Falls back to other values, if some information isn't available. Change it in case of problems - if BIOS provides faulty information about total video memory size, number of planes or number of pages.

Flip requires VBE 1.1. Extended mode info is mandatory since VBE 1.2. Buffering has effect in planar modes only. Fastest buffering can be used if SwapEffect is flip. Buffered variants require Window B to be available. Some performance optimizations are possible, but they aren't implemented yet. Therefore some video modes are slower, than they could be.

SVGA1.drv

All modes are dynamic, i.e. support and parameters of any specific mode is reported by BIOS.

Graphic modes supported: 1bpp, 2bpp, 4bpp, 4bppV, 4bppE, 8bpp, 8bpp direct color, 8bppX, 8bppX direct color, 15bpp, 16bpp, 24bpp and 32bpp RGB/BGR modes are supported.

Text modes supported: 1bppM, MbppM, 1bppT, MbppT, 2bppT, 4bppT.

**Please note!** VBE 1.x implies VGA-compatible video card, as it doesn't provide way to detect VGA-incompatibility. Following features require some degree of VGA compatibility: VSync, some VGA modes, text modes, 4bpp plane modes, 8bpp modes, unchained 8bpp modes. In the worst case scenario only >=15bpp direct color modes with VSync disabled may be available. 

SVGA2Bnk.drv/SVGA2LFB.drv

All modes are dynamic, i.e. support and parameters of any specific mode is reported by BIOS.

Graphic modes supported: 1bpp, 2bpp, 4bpp, 4bppV, 4bppE, 8bpp, 8bpp direct color, 8bppX, 8bppX direct color, 15bpp, 16bpp, 24bpp and 32bpp RGB/BGR modes are supported.

Text modes supported: 1bppM, MbppM, 1bppT, MbppT, 2bppT, 4bppT.

Differences vs SVGA1.drv:
1) Unnecessary code is removed
2) Extended mode info is always available
3) Standard modes aren't supported (non-direct color ones are still supported though)
4) Force32bpp is unsupported
5) Palette control is supported - 8bpp modes aren't disabled by DisableVGABIOS
6) VGA-incompatible cards are supported. It's related to IO ports and standard memory addresses only. BIOS calls shouldn't be affected. Use DisableVGABIOS in case of problems. But, as I understand, planar and banked modes can't even be VGA-incompatible. But we can never be 100% sure. So, they're guarded now.

Compatibility options:
1) DisablePM32: Disable VBE 2.0 32bit protected mode interface, as it can be problematic (especially in case of page flipping). Fall back to BIOS calls or direct bank switching, if supported.
2) DisableVSync: Disable VBE 2.0 VSync support, as it isn't guaranteed to work properly for all swap effectis (only for flipping). Fall back to VGAIO, if supported.

**Windows:**

Windows-specific options, that are shared between all Windows drivers:

**Please note!:** Default settings provide the best possible performance in all situtaions. Mapping algorithms are designed specifically to avoid any hardcoded behaviors. For example arbirtary DIB, system and static palette sizes are supported, not just ordinal 256 colors. Not all option combinations are functional though.

1) PaletteMode. Should palette be enabled? Auto is recommended. Forcing palette off for palette device would cause fallback to default palette. Forcing palette on for RGB device would cause perofmance penalty and depending on Windows version certain features may not even function as expected.
2) RGBPaletteMode. What logical palette should be loaded for RGB video modes, such as 16/24/32bpp modes?
3) DIBPaletteMode. DIB to logical palette mapping. Explicit - we perform mapping ourselves. Implicit - palette manager performs mapping for us. Explicit is quicker, as mapping can be pre-computed, but it requires relying on certain palette manager behavior, so it's less compatible. Even explicit mapping is performed by palette manager itself. Palette manager has several limitations, that can cause wrong results in some cases.
4) LogPaletteMode. Logical to system palette mapping. Explicit - we perform mapping ourselves. Implicit - palette manager performs mapping for us. Explicit is quicker, as mapping can be pre-computed, but it requires relying on certain palette manager behavior, so it's less compatible.
5) IdentityPaletteMode. Identity logical to system palette mapping - is when mapping is like 1, 2, ..,254, 255. Palette manager should skip mapping in this case -> better performance. By default non-identity palette uses "map all entries" color reduction mode, if DIB palette doesn't fit into system one. This can reduce quality for some colors at the end of palette.
6) StaticColorsMode. Static colors limit palette size and prevent identity mapping in some cases. Disabling static colors can affect other applications, but as we always use fullscreen rendering, it shouldn't be problem.
7) ColorReductionMode. What to do if DIB palette doesn't fit into system palette? This can happen in case of using direct color modes, that require full 256 colors palette size. What we do - is try to remap DIB palette to smaller logical palette, that would fit into system palette, or predefined identity palettes, provided by system.
8) StaticSourceMode. From where should we gather static colors for implicit color mapping? System palette may not be available in all cases. For example if static colors are disable or in case of RGB device. Switch to default palette in this case.
9) ClearPaletteMode. For some unknown reason palette manager prefers palette entries, that have never been used before. This can mess our indetity mapping up. Therefore we should "clear" palette via marking all entries as already used. In theory it should be enough to clear palette only once. But option to clear it after every switch to other application is also provided.

For all modes: VSync controls if WM_PAINT or direct rendering is performed, Copy and Swap are supported, NoDoubleBuffer is ignored

GDI.drv
1) 1bpp
2) Mono, emulated
3) 2bpp, emulated
4) 4bpp
5) 8bpp
6) 8bpp Direct color RGB
7) 8bpp Direct color BGR
8) 15bpp (Except Win3x)
9) 16bpp (Except Win3x)
10) 24bpp
11) 32bpp (Except Win3x)

**Please note!** Format support depends on Windows version, specific driver implementation and currently selected video mode. You'll get blank screen, if format is unsupported, garbled colors or distorted image, if it's supported partially. Testing has shown, that some drivers can even support undocumented formats. For example 15/16/32 bit formats can be partially supported by Win3x drivers, despite being officially unsupported by GDI. They aren't implemented in GDI driver now. I'm not sure, if they should be implemented. And if yes - then how they should be implemented, because they're purely GDI specific.

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
