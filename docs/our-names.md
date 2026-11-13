# Our names (SCUS_944.67)

Names the psx-spyro port uses for this executable where they differ from or go beyond this tree's own.
The symbol map (`preparation/symbol_addrs.txt`) keeps the tree's names; ours enter it only where the tree has none. "Port file" is a psx-spyro path.

## Names that differ

| address | this tree | psx-spyro | port file | meaning |
|---|---|---|---|---|
| `0x8001E638` | `Draw` | `BootPrefixFactsFrameDraw` | `titles/spyro3/core/boot_facts.h` |  |
| `0x8004F6C4` | `exe_check` | `DrawSectionFactsCameraBuilder` | `titles/spyro3/core/draw_section.h` |  |
| `0x80055400` | `Update` | `BootPrefixFactsFrameUpdate` | `titles/spyro3/core/boot_facts.h` |  |
| `0x80059444` | `start` | `Crt0Entry` | `titles/spyro3/core/runtime.cpp` |  |
| `0x8005956C` | `VSync` | `RuntimeVSync` | `titles/spyro3/core/runtime.cpp` | libetc VSync: a non-negative argument waits, a negative one returns the count. |
| `0x8005D35C` | `SetGeomOffset` | `LibgteSetGeomOffset` | `titles/spyro3/core/runtime.cpp` | libgte SetGeomOffset, called by the geometry init 0x8002A99C with (0x100, 0x78). |
| `0x8005D96C` | `CdRead` | `RuntimeCdRead` | `titles/spyro3/core/runtime.cpp` | libcd CdRead(dest, src, mode). |
| `0x8005E074` | `CdSync` | `RuntimeCdSync` | `titles/spyro3/core/runtime.cpp` | libcd CdSync, polled by the CD bootstrap leaf 0x80050440 until it reports CS_SELF. |
| `0x8005E0BC` | `CdControl` | `CdCommand` | `titles/spyro3/core/runtime.cpp` | libcd CdCommand(com, parm, result), reached from 0x8002A7D0 with $a0 = 0x0E. |
| `0x800658A0` | `g_Sin` | `RenderGlobalsCameraSineTable` | `titles/spyro3/render/render_facts.h` | 800658A0: the sine table 0x8004E9E4 indexes; 0x8004EA2C reads its cosine a quarter turn on. |
| `0x80065920` | `g_Cos` | `SkyWaveSine` | `titles/spyro3/render/render_facts.h` |  |
| `0x80066FCC` | `lvlIdToIndex` | `LevelIdToIndex` | `titles/spyro3/core/warp.cpp` |  |
| `0x800671A0` | `levelIndexToHomeworldLevelId` | `LevelHomeworlds` | `titles/spyro3/core/warp.cpp` |  |
| `0x80067248` | `g_HudEntries` | `GemCounter` | `titles/spyro3/render/hud_anchor.h` | The widget elements FUN_8002803C registers, and what each one is anchored to. |
| `0x8006C518` | `loadStage` | `LoaderChecksumStage` | `titles/spyro3/core/loader_checksum.cpp` |  |
| `0x8006C530` | `g_Portals` | `PortalsPortalTable` | `titles/spyro3/core/warp.cpp` | Trigger 0x8003FD58's records and the portals its type 6 enters (0x80053F50(index) at 0x80040230). |
| `0x8006C550` | `mobyArrayPtr` | `MobyArray` | `titles/spyro3/core/draw_section.cpp` |  |
| `0x8006C5BC` | `currentLevel` | `LevelId` | `titles/spyro3/core/boot_facts.h` | The level FUN_800584BC stores at 0x80058718. |
| `0x8006DFF8` | `camera` | `DrawSectionFactsProjectionRotation` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006E344` | `game` | `DrawSectionFactsGameState` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006FBFC` | `g_DB` | `DrawSectionFactsBuffer0` | `titles/spyro3/core/draw_section.h` |  |
| `0x80070328` | `spyro` | `DrawMotionSpyro` | `titles/spyro3/render/render_facts.h` |  |

## Names added to the map

| address | added as | was | port file | meaning |
|---|---|---|---|---|
| `0x80017B7C` | `Effect` | `func_80017B7C` | `titles/spyro3/core/runtime.h` |  |
| `0x8001C368` | `SkyFactsEntry` | `func_8001C368` | `titles/spyro3/render/render_facts.h` |  |
| `0x8001C8C8` | `SkyWaveConsumer` | `func_8001C8C8` | `titles/spyro3/render/render_facts.h` |  |
| `0x8001D274` | `DrawSectionPlay` | `func_8001D274` | `titles/spyro3/core/draw_section.cpp` |  |
| `0x8001E460` | `DrawSectionFactsDispatcher` | `func_8001E460` | `titles/spyro3/core/draw_section.h` |  |
| `0x8001FF44` | `CinematicLetterboxEntry` | `func_8001FF44` | `titles/spyro3/render/render_facts.h` |  |
| `0x80022378` | `TerrainFactsEntry` | `func_80022378` | `titles/spyro3/render/render_facts.h` |  |
| `0x800289C8` | `IconEmitter` | `func_800289C8` | `titles/spyro3/render/hud_anchor.h` |  |
| `0x800291B8` | `ValueEmitter` | `func_800291B8` | `titles/spyro3/render/hud_anchor.h` |  |
| `0x800293C4` | `RatioDrawer` | `func_800293C4` | `titles/spyro3/render/hud_slide.h` |  |
| `0x80029708` | `SlideStep` | `func_80029708` | `titles/spyro3/render/hud_slide.h` |  |
| `0x80029904` | `CounterDrawer` | `func_80029904` | `titles/spyro3/render/hud_anchor.h` | The two widget drawers FUN_800285A4 registers, and the two emitters both of them draw through. |
| `0x80029BB0` | `LivesDrawer` | `func_80029BB0` | `titles/spyro3/render/hud_anchor.h` |  |
| `0x8002AB38` | `BootPrefixFactsBootPrefix` | `func_8002AB38` | `titles/spyro3/core/boot_facts.h` |  |
| `0x8002CA50` | `LoaderChecksumLoader` | `func_8002CA50` | `titles/spyro3/core/loader_checksum.cpp` |  |
| `0x8002D0D8` | `TerrainFactsSectorVisibility` | `func_8002D0D8` | `titles/spyro3/render/render_facts.h` |  |
| `0x8002DDA8` | `RenderFactsMobyShadowsEntry` | `func_8002DDA8` | `titles/spyro3/render/render_facts.h` | The close list's drawer, the object pass's fourth call; its texture words sit at the walk's v0 on return. |
| `0x8002E748` | `RenderFactsTextLayoutsEntry` | `func_8002E748` | `titles/spyro3/render/render_facts.h` |  |
| `0x8002E970` | `RenderFactsTextLayoutsEntry_8002E970` | `func_8002E970` | `titles/spyro3/render/render_facts.h` |  |
| `0x80030478` | `MobyFactsEntry` | `func_80030478` | `titles/spyro3/render/render_facts.h` |  |
| `0x80031124` | `RenderFactsMobyDrawerEntry` | `func_80031124` | `titles/spyro3/render/render_facts.h` | jal at 8001EC8C; its translation is the entry's centre, loaded at 800311C8. |
| `0x80033C5C` | `RenderFactsMobyDeferredEntry` | `func_80033C5C` | `titles/spyro3/render/render_facts.h` | The walk's deferred buffer's drawer, the object pass's third call (8001EC94). |
| `0x8003CDA0` | `SpyroDrawerEntry` | `func_8003CDA0` | `titles/spyro3/render/render_facts.h` |  |
| `0x8004E664` | `DrawSectionFactsFlatten` | `func_8004E664` | `titles/spyro3/core/draw_section.h` |  |
| `0x8004E758` | `RenderFactsOverlayLinkEntry` | `func_8004E758` | `titles/spyro3/render/render_facts.h` |  |
| `0x8004E7AC` | `ClearScratch` | `func_8004E7AC` | `titles/spyro3/core/draw_section.cpp` | (address, 0, words) |
| `0x8004F178` | `DrawSectionFactsPositionCopy` | `func_8004F178` | `titles/spyro3/core/draw_section.h` |  |
| `0x80053F50` | `LevelExit` | `func_80053F50` | `titles/spyro3/core/warp.cpp` | The portal entry: an index enters that portal's level; -1 leaves for this level's portal in its homeworld, as the pause menu's Exit Level calls it at 0x80058378. |
| `0x80056434` | `DrawMotionAllocator` | `func_80056434` | `titles/spyro3/render/render_facts.h` |  |
| `0x800584BC` | `WarpToLevel` | `func_800584BC` | `titles/spyro3/core/warp.cpp` |  |
| `0x80065C28` | `g_TerrainFactsQuadCells` | `D_80065C28` | `titles/spyro3/render/render_facts.h` |  |
| `0x80065C38` | `g_TerrainFactsQuadPieces` | `D_80065C38` | `titles/spyro3/render/render_facts.h` |  |
| `0x80065C78` | `g_TerrainFactsQuadCracks` | `D_80065C78` | `titles/spyro3/render/render_facts.h` |  |
| `0x80065CA8` | `g_TerrainFactsQuadCracks_80065CA8` | `D_80065CA8` | `titles/spyro3/render/render_facts.h` |  |
| `0x80065D08` | `g_TerrainFactsPageRemaps` | `D_80065D08` | `titles/spyro3/render/render_facts.h` |  |
| `0x80065D48` | `g_TerrainFactsInnerPoints` | `D_80065D48` | `titles/spyro3/render/render_facts.h` |  |
| `0x80065D58` | `g_TerrainFactsTriangleCells` | `D_80065D58` | `titles/spyro3/render/render_facts.h` |  |
| `0x80065D68` | `g_TerrainFactsTrianglePieces` | `D_80065D68` | `titles/spyro3/render/render_facts.h` |  |
| `0x80065DA8` | `g_TerrainFactsTriangleCracks` | `D_80065DA8` | `titles/spyro3/render/render_facts.h` |  |
| `0x80065E38` | `g_TerrainFactsTriangleCracks_80065E38` | `D_80065E38` | `titles/spyro3/render/render_facts.h` |  |
| `0x80065F58` | `g_TerrainFactsTriangleSubTexture` | `D_80065F58` | `titles/spyro3/render/render_facts.h` |  |
| `0x80065F68` | `g_TerrainFactsPieceTexture` | `D_80065F68` | `titles/spyro3/render/render_facts.h` |  |
| `0x80065FA8` | `g_TerrainFactsPieceShift` | `D_80065FA8` | `titles/spyro3/render/render_facts.h` |  |
| `0x80066028` | `g_TerrainFactsTriangleUvs` | `D_80066028` | `titles/spyro3/render/render_facts.h` |  |
| `0x80066128` | `g_TerrainFactsTriangleUvs_80066128` | `D_80066128` | `titles/spyro3/render/render_facts.h` |  |
| `0x80066228` | `g_TerrainFactsTrianglePieces_80066228` | `D_80066228` | `titles/spyro3/render/render_facts.h` |  |
| `0x80066244` | `g_TerrainFactsQuadPieces_80066244` | `D_80066244` | `titles/spyro3/render/render_facts.h` |  |
| `0x80066274` | `g_IntroCardDeltaTable` | `D_80066274` | `titles/spyro3/render/intro_card_facts.h` |  |
| `0x80066530` | `g_MobyFactsKeyframeBlend` | `D_80066530` | `titles/spyro3/render/render_facts.h` |  |
| `0x80066998` | `g_RenderFactsMobyDeferredPaletteTable` | `D_80066998` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006729C` | `g_LivesCounter` | `-` | `titles/spyro3/render/hud_anchor.h` |  |
| `0x800672F0` | `g_EggCounter` | `-` | `titles/spyro3/render/hud_anchor.h` |  |
| `0x800674AC` | `g_AcrossTable` | `D_800674AC` | `titles/spyro3/render/hud_slide.cpp` | the digits' x arm reads its bytes from here |
| `0x800674E8` | `g_SlideTable` | `D_800674E8` | `titles/spyro3/render/hud_slide.cpp` | bytes, read at 0..0x3B by the icon |
| `0x80069CF8` | `g_LevelNames` | `D_80069CF8` | `titles/spyro3/core/warp.cpp` |  |
| `0x8006B3D0` | `g_CdReadyCallbackPointer` | `D_8006B3D0` | `titles/spyro3/core/runtime.cpp` | libcd's CdReadyCallback word, defaulted by CdInit at 0x8005DB6C. |
| `0x8006B480` | `g_VSyncQueryCounter` | `D_8006B480` | `titles/spyro3/core/boot_facts.h` | Negative VSync reads the libetc vblank count at 0x8006B480 (docs/issues/0160). |
| `0x8006C4F8` | `g_SceneStep` | `D_8006C4F8` | `titles/spyro3/core/draw_section.cpp` | state 0xD draws the pass unless it is 2 |
| `0x8006C554` | `g_DrawMotionParticles` | `D_8006C554` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006C598` | `g_DrawSectionFade` | `D_8006C598` | `titles/spyro3/core/draw_section.cpp` |  |
| `0x8006C5DC` | `g_MobyFactsDrawerParameter` | `D_8006C5DC` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006C5E4` | `g_TransferStep` | `D_8006C5E4` | `titles/spyro3/core/loader_checksum.cpp` |  |
| `0x8006C5F0` | `g_CreditLettersPool` | `D_8006C5F0` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006C600` | `g_DrawSectionFactsCurrentBuffer` | `D_8006C600` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006C634` | `g_DrawSectionFactsOrderingTable` | `D_8006C634` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006C638` | `g_RenderGlobalsOverlayPair` | `D_8006C638` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006C644` | `g_SkyWaveTick` | `D_8006C644` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006C64C` | `g_CinematicLetterboxHeight` | `D_8006C64C` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006C65C` | `g_DrawSectionSparx` | `D_8006C65C` | `titles/spyro3/core/draw_section.cpp` | Sparx's record, 0 while he is absent |
| `0x8006C664` | `g_DrawSectionFactsPrimitiveCursor` | `D_8006C664` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006C668` | `g_DrawSectionFactsScratchEnd` | `D_8006C668` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006C6B0` | `g_ChainTail` | `D_8006C6B0` | `titles/spyro3/core/draw_section.cpp` |  |
| `0x8006C6B4` | `g_LoaderChecksumSum` | `D_8006C6B4` | `titles/spyro3/core/loader_checksum.cpp` |  |
| `0x8006C6B8` | `g_LoaderChecksumCursor` | `D_8006C6B8` | `titles/spyro3/core/loader_checksum.cpp` |  |
| `0x8006C718` | `g_DrawSectionFactsGate` | `D_8006C718` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006C788` | `g_GlyphImages` | `D_8006C788` | `titles/spyro3/render/hud_slide.cpp` | word: 8-byte glyph images |
| `0x8006C7D4` | `g_DrawSectionFactsBinMark` | `D_8006C7D4` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006C7DC` | `g_DrawSectionFactsScratchSize` | `D_8006C7DC` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006D048` | `g_TerrainFactsSectorTable` | `D_8006D048` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006D04C` | `g_TerrainFactsSectorCount` | `D_8006D04C` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006D05C` | `g_PortalsTriggerTable` | `D_8006D05C` | `titles/spyro3/core/warp.cpp` | Trigger 0x8003FD58's records and the portals its type 6 enters (0x80053F50(index) at 0x80040230). |
| `0x8006D068` | `g_TerrainFactsTextureTable` | `D_8006D068` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006D074` | `g_TerrainFactsFarDepth` | `D_8006D074` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006D078` | `g_TerrainFactsVisibleSectorCount` | `-` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006D07C` | `g_TerrainFactsFogColour` | `D_8006D07C` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006DEF8` | `g_DrawMotionGlows` | `D_8006DEF8` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006E00C` | `g_DrawSectionFactsViewRotation` | `D_8006E00C` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006E020` | `g_DrawSectionFactsCameraPosition` | `D_8006E020` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006E02C` | `g_DrawSectionFactsDrawCameraPosition` | `-` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006E038` | `g_TerrainFactsFogLevel` | `D_8006E038` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006E03C` | `g_DrawSectionFactsCameraAngles` | `D_8006E03C` | `titles/spyro3/core/draw_section.h` |  |
| `0x8006E044` | `g_CameraMode` | `D_8006E044` | `titles/spyro3/core/boot_facts.h` | Camera controller FUN_800144B4's mode and sub-state. |
| `0x8006E048` | `g_CameraSubState` | `D_8006E048` | `titles/spyro3/core/boot_facts.h` |  |
| `0x8006E1F4` | `g_DrawMotionSprites` | `D_8006E1F4` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006E334` | `g_SkyFactsSectors` | `D_8006E334` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006E33C` | `g_RenderFactsMobyDeferredFogColour` | `D_8006E33C` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006E388` | `g_MobyFactsExitV0` | `D_8006E388` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006E390` | `g_MobyFactsCloseCursorHome` | `-` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006E588` | `g_TerrainFactsFoggedColours` | `D_8006E588` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006EDA0` | `g_SkyWaveWave` | `D_8006EDA0` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006EE2C` | `g_MobyFactsMeshSlotTable` | `D_8006EDB8` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006FBAC` | `g_DrawMotionShadow` | `-` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006FBC8` | `g_LevelLoadStep` | `D_8006FBC8` | `titles/spyro3/core/draw_section.cpp` |  |
| `0x8006FC70` | `g_DrawSectionFactsBuffer1` | `D_8006FC70` | `titles/spyro3/core/draw_section.h` |  |
| `0x80070134` | `g_SparxShown` | `D_80070134` | `titles/spyro3/core/draw_section.cpp` | byte |
| `0x8007020E` | `g_SecondStart` | `D_8007020E` | `titles/spyro3/core/loader_checksum.cpp` | Second range: one byte a step, then the end mark stage 7 waits for. |
| `0x80070260` | `g_DrawMotionMeshes` | `D_80070260` | `titles/spyro3/render/render_facts.h` |  |
| `0x80070610` | `g_DrawMotionTrails` | `D_80070610` | `titles/spyro3/render/render_facts.h` |  |
| `0x80071540` | `g_RenderGlobalsRegisterSaveArea` | `D_80071540` | `titles/spyro3/render/render_facts.h` |  |
| `0x8007179C` | `g_DrawMotionFlame` | `D_800716B0` | `titles/spyro3/render/render_facts.h` |  |
| `0x800719CC` | `g_FirstDigit` | `D_800719CC` | `titles/spyro3/render/hud_slide.cpp` | halfword: the image of digit 0 |
| `0x80072330` | `g_RenderGlobalsVisibilityGroups` | `D_80072330` | `titles/spyro3/render/render_facts.h` |  |
| `0x80072430` | `g_DrawMotionBeams` | `D_80072430` | `titles/spyro3/render/render_facts.h` |  |

## Code sites

Addresses inside a function (return addresses, branch joins) the port hooks or reads.

| address | function + offset | port name | port file | meaning |
|---|---|---|---|---|
| `0x8001C3A0` | `func_8001C368+0x38` | `SkyFactsVisibilityCallSite` | `titles/spyro3/render/render_facts.h` |  |
| `0x8001EC94` | `func_8001EC5C+0x38` | `RenderFactsMobyDrawerFieldPassReturn` | `titles/spyro3/render/render_facts.h` |  |
| `0x800223C8` | `func_80022378+0x50` | `TerrainFactsVisibilityCallSite` | `titles/spyro3/render/render_facts.h` |  |
| `0x8006085E` | `func_80060844+0x1A` | `FirstEnd` | `titles/spyro3/core/loader_checksum.cpp` |  |

## Overlay addresses

Addresses in the WAD overlay range; they need the overlay's own config before they enter a map.

| address | port name | port file | meaning |
|---|---|---|---|
| `0x80074380` | `StateHook` | `titles/spyro3/core/draw_section.cpp` |  |
| `0x80074488` | `SceneHook` | `titles/spyro3/core/draw_section.cpp` |  |
| `0x80076FA6` | `SecondEnd` | `titles/spyro3/core/loader_checksum.cpp` |  |
| `0x8007B6E4` | `LoaderChecksumDone` | `titles/spyro3/core/loader_checksum.cpp` |  |
| `0x8007F12C` | `TitleState` | `titles/spyro3/core/boot_facts.h` | Title image data, resident whenever the game state is the title's: the state byte and its step byte. State 1 runs the Insomniac credit at step 0 and holds the finished logo while "press start" waits at step 1. |
| `0x8007F12E` | `TitleStep` | `titles/spyro3/core/boot_facts.h` |  |
