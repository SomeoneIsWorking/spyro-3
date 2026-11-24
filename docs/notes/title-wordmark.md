# Title wordmark

`WAD.WAD` entry 6 (directory word pair 6 at +0x30: offset 0x57800, length 0xB6000) holds at +0x800 a 512-halfword-wide
block that lands as VRAM (512, 0) onward: VRAM row r is the entry's 0x400 bytes at +0x800 + 0x400 * r.

The title screen draws the SPYRO YEAR OF THE DRAGON wordmark as one semi-transparent POLY_FT4 (code 0x2E), tpage
`0x88` (8-bit, page (512, 0)), CLUT word `0x0020` (VRAM (512, 0), the block's first row), uv (0, 1)..(190, 75):
190 x 74 texels drawn 1:1 at x 161..351. Colour 0 is transparent. Read from the packets in RAM at the title.
