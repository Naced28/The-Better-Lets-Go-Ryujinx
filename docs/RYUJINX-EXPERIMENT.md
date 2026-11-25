# Ryujinx compatibility experiment

## Target and status

- Game: Pokémon: Let's Go, Pikachu! 1.0.2
- Build ID: `C208DB6A4EF4361F28B8402BE0F7CD9A`
- Tested emulator: Ryujinx 1.3.3 on Windows, Vulkan
- Current candidate: v8, experimental and not yet tested in-game

The owner confirmed that the v5 diagnostic build could enter a wild battle, perform an attack and proceed from a Bag Poké Ball to the game's native capture screen. The v6 build restored the custom Options rows and then crashed while displaying them. Its log showed an invalid access at `0xC541000`; the guest stack passed through the patch's custom text handler and the game's text append routine. No raw user log is included in this repository.

The v8 candidate removes the custom Options UI, forces ordinary wild encounters to use the battle mode regardless of the saved Off bit, keeps the v5 battle-to-capture result hooks, and restores the two EXP-on-win gates at `0x9D8A44` and `0x9D8A5C`. **EXP after a K.O. has not yet been tested with v8.** The patch builds cleanly and its IPS32 structure and target Build ID have been checked; those checks do not replace an in-game test.

## What is enabled or unavailable

- Ordinary wild encounters start battles automatically; there is no in-game toggle in this build.
- Choosing a Poké Ball in the battle Bag is intended to proceed to the native catch screen.
- The EXP-on-win gates are patched, awaiting confirmation that a K.O. awards EXP.
- The custom Options rows and their text resolver are omitted to avoid the observed menu crash.
- The diagnostic build leaves the original faint animation, Exp. Share fighter tracking and post-catch EXP messaging paths in place. The mod's Exp. Share Off behavior is therefore not validated here.
- Target is Pikachu 1.0.2 only. Do not use this IPS with Eevee or another game build.

## Install

Use only the Ryujinx archive for this test candidate. Disable any other Better Let's Go or wild-battle patches first, then add the ZIP with Ryujinx's mod manager and restart the game. Back up the save before testing.

## Rebuild

The builder requires your own decompressed `main` for Pikachu 1.0.2, retaining its 0x100-byte NSO header, and Python with Capstone installed. Do not commit game files, keys, save files or logs.

```powershell
$env:TBLG_DIAGNOSTIC_NO_OPTIONS = '1'
$env:TBLG_DIAGNOSTIC_KEEP_FAINT_SOUND = '1'
$env:TBLG_DIAGNOSTIC_CORE_BATTLE = '1'
python tools/build_patch.py path/to/main.decompressed output.ips
```

The builder checks the Build ID and every patched original instruction before writing the IPS32 file. See [the technical notes](TECHNICAL.md) for the address map and patch design.
