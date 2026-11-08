# Immortals Fenyx Rising (`01004A600EC0A000`)

Update 1.3.4 (v720896) over the supplied base game, SDK 10.4.0, Ubisoft's Anvil engine (Scimitar) on NVN, with Wwise. The loaded modules are `main` and `sdk`. Nested DLC packages were left out of this pack.

Mac gameplay is not yet tested: the packer's region check saw no address regions in its one-second window. iOS is unvalidated.

## Memory

- The NPDM declares 8 MB of system resource (virtual address memory) and `main` never sets a heap. The profile keeps the survey's 5 GB guest block, with a 4.375 GB alias region and 256 MB stack region, where the game maps its memory itself.
- **Open:** the layout is unmeasured under play. A later region check after a real boot may need a larger alias region.

## Files and shaders

- The merged RomFS holds hundreds of Scimitar `.forge` files. Only the `*_nvn.forge` packages carry GPU programs; the rest are world data and are left out of the loose scan so the split does not read them.
- **Resolved: no shaders found.** [GPUCODEONLY records in Scimitar nvn forges](../../../docs/reference/shaders.md#gpucodeonly-records-in-scimitar-nvn-forges). Nine `*_nvn.forge` packages hold the NVN programs as GPUCODEONLY records (Maxwell code, then the 0x880-byte control). Anvil blocks are Oodle Mermaid, decoded with the game's own decoder in the Mac host. Programs hold one stage; vertex shaders take the single-stage cover.
- The split finds 19,603 unique shaders: 12,377 vertex, 7,210 pixel, 8 hull and 8 domain. All translate and compile for the Mac. There is no pipeline prebuild list yet (`pso_manifest.tsv` is empty).

## Mac testing

The NSP script's `--platform mac` pack completes and writes Mac libraries for every shader. A boot past the region check, the title screen and any in-game scene are still open.

## iOS build

Not built or tested.

## Found on this game

- [GPUCODEONLY records in Scimitar nvn forges](../../../docs/reference/shaders.md#gpucodeonly-records-in-scimitar-nvn-forges).

## Open

- First boot, title screen and gameplay on the Mac.
- Measure the alias region under play; the 5 GB survey layout is unconfirmed.
- Nested DLC.
- iOS testing is performed by the user.
