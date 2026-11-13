# Prior art

Outside work on Spyro: Year of the Dragon (USA) rev 0 `SCUS_944.67`, SHA-1 `31ad35fd03539910b5b3d9309ae52f5acaf3612e`, the build this tree matches. A reference names addresses; the psx-spyro
port's measurement decides behaviour. Address checks ran `decomp_pipeline.py --function-at` on our images
(2026-10-13); licences are GitHub SPDX ids; push dates checked 2026-11-13. Submodule pins named below are psx-spyro's
(2026-11-13, before this tree became its fork).

| project | URL | kind | license | target build | build match (addresses checked) | what we may take | notes |
|---|---|---|---|---|---|---|---|
| TheMobyCollective/spyro-3 | https://github.com/TheMobyCollective/spyro-3 | matching decomp (splat), EXE plus encrypted WAD overlays | CC0-1.0 | Spyro 3 `SCUS_944.67` rev 0 | matched: `preparation/scus_944.67.yaml` sha1 `31ad35fd…` equals ours; `main` segment starts at our game main `0x8001200C` (Ghidra, 12 insns); `func_8001E638` tagged Draw (our draw, 349 insns); `func_80055400` (our update), `func_8002AB38` (our boot prefix, 178 insns) listed | code and names (CC0), copied with attribution | Submodule `external/spyro-3` pin `b0246319` (push 2026-11-13). `progress/exe.md` 180 of 337 EXE functions matched (was 164 on 2026-10-13); 1,178 `.c` files including level and cutscene overlays. README notes modchip and anti-crack protection and encrypted overlays, relevant to the `jal 0x80074DEC` outside resident text. |
| wafflewizard1/SpyroGhidra | https://github.com/wafflewizard1/SpyroGhidra | Ghidra `.gzf` plus exported C, Spyro 1, 2, 3 1.0 NTSC | none | Spyro 2 NTSC, Spyro 3 1.0 NTSC | matched: Spyro 2 export has `FUN_80011e9c`, `FUN_80043858`, `FUN_80023bb4`; Spyro 3 export has `FUN_8002a834` and calls `FUN_8002ab38` and `FUN_8005d35c(0x100,0x78)` | names only | Dormant since 2024. Never import the `.gzf`; read the `.c` text only. |
| ArsonAssassin/S3AP | https://github.com/ArsonAssassin/S3AP | Archipelago randomizer client for Spyro 3 | MIT | Spyro 3 (region and revision not checked) | not checked | RAM addresses (MIT), copied with attribution after measurement | Last push 2025-09-18. |
| wafflewizard1/Spyro-3-Recompiled | https://github.com/wafflewizard1/Spyro-3-Recompiled | static recompilation (psxrecomp) with an interpolation layer (`spyro3/spyro3_interpolation.c`) | none | Spyro 3 `SCUS-94467` | not checked: serial only | nothing | Built on the noncommercial psxrecomp runtime; README calls it buggy. Last push 2026-08-09. |
| FranklyGD/Spyro-Scope | https://github.com/FranklyGD/Spyro-Scope | live RAM and data viewer | GPL-3.0 | Spyro 1 NTSC-U, Spyro 2 NTSC, Spyro 3 NTSC v1.1 | not checked; Spyro 3 v1.1 is not our rev 0 | evidence only | Data-format reference; its terrain collision format (flag byte, water bit, slope) informs `docs/plans/more-vegetation.md`. |

Not found (2026-11-13): source for any Spyro 2 or 3 widescreen or 60 fps patch (the PCSX2-forum Spyro 3 widescreen
code targets NTSC-U v1.1, not our rev 0); a Spyro title on decomp.dev; a decomp of the sequels beyond the
TheMobyCollective splits. Searched GitHub repositories (titles, serials, "decomp", "recomp", "port", "widescreen",
"60fps"), decomp.dev and the web.

Not found (2026-11-12, for G006): any foliage, grass-density or vegetation mod for the PlayStation Spyro titles or
Reignited, or a grass-density enhancement in a decomp-based port of another title.
