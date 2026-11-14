# RE frontier — Spyro: Year of the Dragon (`SCUS_944.67` rev 0)

The ordered evidence chain the psx-spyro port follows toward faithful behaviour, run with re-harness
`re_frontier.py` from this repository's root (from the port: `RE_FRONTIER_ROADMAP=external/spyro-3/docs/re-frontier.md`).
`where` and evidence paths (`game/...`, `titles/...`, `docs/issues/...`) are psx-spyro paths. A dependency on a step
kept in another title's roadmap is named in `notes` as `cross-title dep`, not in `deps`.

Statuses: ✅ re-verified · 🟡 re-partial · 🔬 in-progress · ⬜ todo · ➖ skip-by-design · ⏸ blocked
(computed). A failure must refuse loudly rather than selecting an alternate execution method.

<!-- Machine-edited by re-harness tools/re_frontier.py add/set. Format: `## <area>` sections;
     each entry is `### <id> — <title>` followed by `- <field>: <value>` lines. -->

## titles

### spyro3.identity — Preserve Spyro 3's independent executable facts
- status: re-partial
- deps:
- evidence: `SCUS_944.67` has its own manifest, serial, entry, size, and digest facts. It now also executes: `tools/title_route.py --title spyro3` reaches the guest's playing state from its own title screen (observed states 0,11,5,6,5,6,5,6,5,3,0; arrival at 4890 fields) and the guest's own position words move under pad input (walk 1405 units, jump z 18513 -> 18710), with 0 faults and 0 interpreter fallback.
- where: titles/spyro3/executable.json; titles/spyro3/core/runtime.*
- gap: Disc provenance remains unverified; no level words are recorded for this title, so the route proves MOVEMENT but not which level it is in.
- notes: Spyro 3 implementation waits for Spyro 1's representative gameplay gate. cross-title dep: boot.provision (open-spyro).

### spyro3.widescreen — Widen Spyro 3's own guest projection
- status: re-partial
- deps: spyro3.identity
- evidence: every site was measured in Spyro 3's own image, not copied from Spyro 2: `SetGeomOffset` leaf `0x8005D35C`, whose sole CR26 publication is `0x8005955C` (that one writes the projection distance H and is deliberately NOT intercepted), plus four inline CR24/CR25 restatements at `0x80033EF8`, `0x80033EFC`, `0x80034B30`, `0x80034B38`; on Record the centre stays retail's and the canvas holds the margins, so none is rewritten. Authored window 512x240, OFX 256, OFY 120, H `0x155`. The shared owner latches from the guest's own published display mode and reports `aspect=16:9 presentation 684x240 (margin 86px), projection 512x240 (margin 86px, centre X 342)`, and a presented in-level capture shows the widened scene with the player unchanged in size.
- where: titles/spyro3/core/runtime.*; game/core/runtime.*
- gap: the single `SetGeomOffset` call the route makes is INCOMPARABLE under the override differential ("original path performed platform-service @0x8005D35C"), so the leaf is not yet shown equal to retail; it is also called only once in the whole route.

### spyro3.moby-visibility — Own Spyro 3's moby visibility walk natively
- status: re-partial
- deps: spyro3.identity
- evidence: `0x80030478` (811 insns, matching Spyro 2's `0x80043858` in size) walks the same 0x58-byte records through the same sphere-frustum logic, including the `4*x - 3*z` term. Override differential at 4:3 over the in-level route: 26/26 sampled calls match retail, 0 mismatches. A longer route (3000 steps, every 4th call) found `v0`/`v1` left by the crack and piece emitters differing from retail (13/197); with the emitters' result registers fixed: 378/378.
- where: game/render/field/guest_moby_*; titles/spyro3/render/render_facts.h
- gap: none on this route.

### spyro3.terrain-drawer — Own Spyro 3's terrain drawer natively
- status: re-partial
- deps: spyro3.identity
- evidence: `0x80022378` (5487 insns, matching Spyro 2's `0x80023BB4`), with the sector-visibility leaf `0x8002D0D8` called from `0x800223C8`, the visible-sector count at `0x8006D078`, outcodes `0x000D0000`/`0x00E40000`/`0xFE00`/`0x02000000`, and the caller analogue at `0x8001EC24`. Override differential at 4:3 over the in-level route: 26/26 sampled calls match retail, 0 mismatches. A longer route (3000 steps, every 4th call) found `v0`/`v1` left by the crack and piece emitters differing from retail (13/197); with the emitters' result registers fixed: 378/378.
- where: game/render/terrain/guest_terrain_*; titles/spyro3/render/render_facts.h
- gap: the margin objects the widening reveals are not shown to be ANIMATED from object memory; only their rendering is covered.

### spyro3.record — Present Spyro 3 from its frame record with keyed terrain
- status: re-verified
- deps: spyro3.terrain-drawer
- evidence: the drawer's caller `0x8001EC24` passes `$a1 = 0` (the object key) and `$a0` = the scratch end, which alternates with the double-buffered pool. The draw `0x8001E638` switches on game state `0x8006E344` (`lw` at `0x8001E6E0`); level id `0x8006C5BC` is stored by `FUN_800584BC` at `0x80058718`. Camera controller `FUN_800144B4` runs the same mode machine as Spyro 2's `FUN_8001FA58` over mode `0x8006E044` and sub-state `0x8006E048`. The flatten is `0x8004E664`; states 4 and 0xD chain a second pass whose flattens return to `0x8001EA40` and `0x8001EB4C` and must not reassign bins. Between a field's draw and its present the guest rewrites level words the drawer reads (sector data near `0x800867D0`, `0x800896BC`, `0x80091088`, landed by the per-frame update's CD path under `0x8004FA24`), which the replay of the draw body reads live.
- where: titles/spyro3/render/render_facts.h, titles/spyro3/core/{runtime,draw_section}.*; game/core/{frame_cut,draw_section}.*; game/render/terrain/guest_depth_bins.*
- gap: what streams the rewritten sector words (CD read target and its owner in `FUN_8004FA24`) is not traced further than the watchpoint.
- notes: cross-title dep: guest.camera-controller (spyro-2).

### spyro3.hud-anchor — Anchor Spyro 3's in-level HUD at the widened edges
- status: re-partial
- deps: spyro3.widescreen
- evidence: the HUD pass is `0x80029E48`, called from `0x8001E460` under bit `0x20`, dispatching one drawer per widget through the table at `0x8006727C` that `0x8002803C` fills; `0x800285A4` registers three groups — `FUN_8002803C(0x40, 3 widgets, init 80027E40, step 80027A60, DRAW 80029904, value *0x8006C71C)`, `(0x41, 4 widgets, init 80027E40, step 80027B0C, DRAW 80029BB0, value *0x8006C784)` and `(0x42, 5 widgets, init 80027E40, step 80027A60, DRAW 80029904, value *0x8006C660)`. Each drawer computes its X from the element's first short and emits an ICON through `0x800289C8(icon, x)` and a VALUE through `0x800291B8(value, x, y, digitWidth)`. Measured elements and classes: collectable counter `0x80067248` authored x 20 y 28 (LeftEdge), lives counter `0x8006729C` authored x 256 y 28 (Centred, authored ON 0x100), egg counter `0x800672F0` authored x 492 y 28 (RightEdge). Classification CANNOT be by return address on this title: both counters are drawn by `0x80029904` and reach the SAME two emitter call sites — measured in one frame, the icon emitter's ra is `0x800299B8` for the gem at x 20 AND the egg at x 382, and the value emitter's ra `0x800299E4` for both (x 61 and x 423) — so the element is carried down one level by `spyro3::hud_anchor::DrawState`. The icon emitter is NOT corrected on every call either: `FUN_800291B8` draws its digits by CALLING `FUN_800289C8` once per glyph from `0x80029374` (return `0x80029378`), so correcting the value emitter and then those glyphs applies the margin TWICE — measured at 684, the collectable count lands at x -111 instead of -25 and is drawn off the left edge so the number is absent, and the egg's icon lands at 595 instead of 468 and is jammed against the right edge, which reads as the icon and the count having swapped sides; the value emitter therefore opens `DrawState::insideValue` and the icon emitter leaves that interval alone. Presented evidence at 684x240 after the fix: collectable icon columns 21..49 against 20..50 at 4:3, its digit 61..84 against 61; egg digit 595..618 against 423..446, i.e. +172 = the full widening; icon left of count on both sides; lives centred; 4:3 capture PIXEL-IDENTICAL to the pre-change reference, 0 of 122880 pixels differing.
- where: titles/spyro3/render/hud_anchor.*
- gap: the meter's absence is not re-measured for this title, and widgets shown only by the `0x41`/`0x42` state functions under other game states have not been enumerated.

### spyro3.story-pictures — Spyro 3's intro story pictures are authored 4:3 stills
- status: re-grounded
- deps: spyro3.identity
- evidence: the story overlay (state word `0x8006C5E4`) loads each captioned shot as a 512x256 15-bit picture with LoadImage `0x8005A478` at `0x80074D28` (RECT 512,0,512,256 from `[0x800722C0]`) and `0x80074D6C` (RECT 512,256 from +0x40000), then draws it as four 128x216 sprites (tpage `E1000508..0E`) at (0..511, 12) with the caption over it; no GTE work runs while it shows. Issue 0234.
- where: guest only (overlay at `0x80074xxx`)
- gap: none; the pictures are kept at 4:3 by decision (issue 0234).

### spyro3.moby-drawers — Spyro 3's moby mesh drawers
- status: re-partial
- deps: spyro3.moby-visibility
- evidence: the moby walk `0x80030478` does not project its mobys: it writes a 0x44-byte render-list entry (record at +0x40, mesh at +0x04, rotation at +0x28) and hands the list base to the guest in GTE data registers (VXY1 = scratch base - 0x3000, VZ1 = the parked parameter at `0x8006C5DC`). The three moby mesh drawers are `0x80031124`, `0x80033C5C` and `0x8002DDA8`, the three calls `FUN_8001EC5C` makes straight after the walk, one per list the walk builds; `0x8003CDA0` behind the state guard is the 2D/overlay pass. Each is one guest call over its whole list, with the per-moby loop inside it (`FUN_80031124` alone is 2153 lines of Ghidra C).
- where: titles/spyro3/render/render_facts.h
- gap: none for interpolation: the drawers run inside the field redraw (spyro2.field-redraw), which re-runs them at the in-between's inputs; they stay guest code.

### spyro3.text-font — Spyro 3's 2D text font and button icons
- status: re-verified
- deps: spyro3.identity
- evidence: FUN_8002E748 (sprites) and FUN_8002E970 (quads), decompiled from SCUS_944.67, are Spyro 2's two layouts over this image's words: cursor *0x8006C664, pair *0x8006C638, g_TextGlyphCells 0x800666F0, g_TextEscapes 0x800667F0..0x8006681E, g_TextColours 0x80066820; the same texture page 0xE1000618, CLUT words 0x4922 (text) and 0x4962 (icons) and the same cell grid. Against Spyro 2 the table adds '+' (cell 130) and '=' (cell 51) and narrows eleven capitals' and h's advance by one, t's widens by one. Icons '<' Cross, '>' Square, '{' Circle, '}' Triangle, from WAD.WAD strings 'Press the < button to jump', 'just jump, then press the } button in the air' (stomp), 'Press > or { to kick enemies'. A raw VRAM dump of the page shows cells 105-108 as the cross (index 1), square (2), circle (4) and triangle (3), one index each and unshadowed, cell 130 the '+', and the other cells as Spyro 2's. Letters shade down the cell through indices 5 8 7 3 9 6 4 a b (1 and c the darkest few) over a drop shadow one texel right and below in index 2, the one index no texel of which has an empty texel up-left of it (letter cells 0-20, 32-52, 64-83).
- where: game/render/overlay_pair.*; game/render/text_font.h; titles/spyro3/render/render_facts.h
- gap: none
- notes: cross-title dep: spyro2.text-font (spyro-2). Plans 0206 and 0207 replace these cells at present time.
### spyro3.atlas-font — Spyro 3's Atlas book font
- status: re-verified
- deps: spyro3.text-font
- evidence: read from main RAM with the Atlas open (Sunrise Spring, pause, Atlas). The Atlas code lies at 0x80075FBC-0x80076A80 while it shows. Its string drawer 0x80076228(string, x, y, colour) maps each byte through 0x80075FBC to a glyph index and draws it with the icon emitter 0x800289C8(&icons[index], x, y + lift), icons = *(SpriteData **)0x80070108, then sets the packet's colour word to `colour` for an index below 0x9F. A SpriteData is 8 bytes: u0, v0, u16 CLUT, u1, v1 (both inclusive), u16 DR_TPAGE; 0x800289C8 draws it as one POLY_FT4 (0x2C, 0x2E unless tpage bits 5-6 are 0x60). Indices: a-z 0x42-0x5B, A-Z 0x5C-0x75, 0-9 0x76-0x7F, then ' : , ! . ? / % at 0x80-0x87, '[' ']' '{' '}' at 0x9F-0xA2 (the Triangle, Square, Circle and Cross icons, u 12, 24, 36, 48 at v 114, in their own CLUTs 0x1A72, 0x1D2C, 0x1D6C, 0x1DAC), and '@' an escape whose next byte goes through 0x80076128 (jump table 0x80075660): ! ? S C c to 0x88-0x8C (whole glyphs), A a B b G g H h U u V v I i J j T t to 0x91 0x92 0x93 0x94 0x8D 0x8E 0x8F 0x90 0x95 0x96 0x97 0x98 0x99 0x9A 0x9B 0x9C 0x9D 0x9E (marks). Advances are the bytes at 0x8007B01A + index (0x80076430 measures with them); one of 0x80 or more is instead an x offset of byte - 0x100 with no advance, so the marks 0x8D-0x9E draw over the letter before them, lifted 4 (0x8D 0x8F 0x91 0x93 0x99 0x9B) or 1 (0x8E 0x90 0x92 0x94 0x9A) texel more; an unmapped byte advances 6; g p q y draw 3 lower, . , / % 1 lower. All glyphs are 12x9 (j 12x12) through CLUT 0x09F2, on the 4bpp pages DR_TPAGE 0x09-0x0D (x 576-832, y 0), u0/v0 per glyph in the table at icons + 8 x index (0x801B2508 in that run): a at (12, 24) on 0x09, e-i on 0x0C, A-Z and digits spread over 0x09-0x0C. The Contents caller picks the colour at 0x80076958-0x80076984: 0x0D8CCC, 0x78898C, or 0x202020 where the byte at 0x80071FB0 + row is set.
- marks: read from the page in VRAM with the Atlas open: 0x88-0x8C are ¡ ¿ ß Ç ç, 0x8D-0x90 a grave, 0x91-0x94 an acute, 0x95-0x98 a diaeresis, 0x99-0x9C a circumflex, 0x9D-0x9E a tilde (so @G/@H grave, @A/@B acute, @U/@V diaeresis, @I/@J circumflex, @T tilde; the pairs differ only in their x offsets). The letters are one index (4) each; 0x9F-0xA2 are the PlayStation buttons in several colours.
- shadow: there is no shadow pass. The drawer 0x80076228 is called three times (0x8007668C the heading in 0x202020, 0x800769BC and 0x80076A38 a row in the colour 0x80076958 picked), each string once with no offset copy; the 0x202020 quads are the heading and the rows that byte marks.
- table: the SpriteData entries 0x42-0xA2 of *0x80070108 read the same in Sunrise Spring and Midday Gardens (RAM dumps with the Atlas open). The HUD's digit table *0x8006C788 (digits from the halfword at 0x800719CC, read by the value emitter 0x800291B8) is a different table whose entries move with the level: 0x8018C7EC with digits 2-9 on DR_TPAGE 0x0A in Sunrise Spring, 0x80190DBC with them on 0x0C and 0x1F in Midday Gardens.
- where: — (port: psx-spyro titles/spyro3/render/sprite_fonts.h)
- gap: none

### spyro3.loading-picture — Spyro 3's level loading picture and the load under it
- status: re-verified
- deps: spyro3.identity
- evidence: UpdateLoadingImage 0x80058778 sub-state 0 reads and LoadImages picture loadImg[cursorPos 0x8006FBCC] at count 0x8006FBC4 0, increments the count before the draw 0x80059038 lights it count*16, and leaves for sub-state 1 on reading 0xD. Sub-state 3 of the same update enters a level only for cursorPos 0..4 (FUN_80053944 path); 5 on are the story cards (New Game is 6, the cutscene cards after it 14, 15). The fade-out loop 0x80020168 (pass count in $s0, VSync(0) return 0x80020270) is called only from the draw 0x80059038 sub-state 3 (jal 0x8005933C). Loader 0x8002CA50 stage 0 calls ResetHuds 0x800282D8, whose SetHud/sprite lookup walks the table at [0x8006C738] in GetSpriteIndex 0x80027934 (loop at 0x80027958) for class -1: from the title screen the pointer is 0x800A2C7C and the walk costs 1.96M cycles, about 3.5 fields of guest CPU before the stage-0 read is issued. Stage 8 tests the code checksum 0x8006C6B4/0x8006C6B8 and zeroes random words at func_8002AB38 on a mismatch.
- evidence: stage 7 (func_loading_8007494C case 7) needs nothing the count-0 update leaves behind: it moves on once the autosave func_loading_80077438 returns non-zero (state 4 from the title returns 1) and the checksum cursor 0x8006C6B8 is 0x8007B6E4. What the count-0 update does for the load is its CDLoadSync's `while (CDLoadTime())` spin: CDLoadTime 0x800503F8 calls CDMusicUpdate 0x8004FA24 and returns 1 while 0x8006E48C is non-zero, so WarpToLevel's music stop (musicEnabled 0x8006E49C set, the XA stream faded 8 -> paused 9 -> idle 0, two CdlPause) runs to the end inside that one update before the picture read. With the count-0 update skipped, the loader's own polls carry the stop (stage 0 waits while CDLoadTime returns 1), and the read stage 6's step issues after a CdlPause from the stop stays in flight until CDLoadTime's own timeout (readTime 0x8006E484 reaching maxReadTime 0x8006E488 = sectors + 0x78) re-issues it: stage 7 held 75 updates in the port (psx-spyro scratch/loadpic2/skip2, skip4). The picture's read, LoadImage and DrawSync feed only its draw. Each update increments 0x8006FBC4 after its sub-state's work, so the count-0 update's own draw lights the picture at count 1, 16/128; DrawLoadingImage at count 0 runs func_8001EBAC, which clears VRAM rows 0-240 and 228-468, both display buffers, to black.
- where: titles/spyro3/core/boot_facts.h; game/core/counted_screen_skip.*; titles/spyro3/core/loader_checksum.cpp
- gap: none
- notes: psx-spyro issue 0248
