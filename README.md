# The Better Let's Go — Ryujinx experimental fork

This repository is a Ryujinx compatibility fork of **[The Better Let's Go](https://github.com/feelingdev/The-Better-Lets-Go)** by [feelingdev](https://github.com/feelingdev). The upstream project adds wild battles and other gameplay changes to Pokémon: Let's Go. Please visit the upstream repository for its original documentation, Switch/Atmosphère builds, and full feature list.

This fork contains experimental compatibility work for **Pokémon: Let's Go, Pikachu! v1.0.2** on Ryujinx. It is not an official upstream release.

## Current test build

The latest candidate is **v8**, available from the [Ryujinx v8 test release](https://github.com/Naced28/The-Better-Lets-Go-Ryujinx/releases/tag/ryujinx-v8-test).

| Item | Value |
|---|---|
| Game | Pokémon: Let's Go, Pikachu! |
| Game version | 1.0.2 |
| Title ID | `010003F003A34000` |
| Build ID | `C208DB6A4EF4361F28B8402BE0F7CD9A` |
| Emulator tested | Ryujinx 1.3.3, Windows 11, Vulkan |
| Status | Experimental; test results below are incomplete |

### Behavior in this fork

- Ordinary wild encounters start battles automatically. There is no in-game switch in this build.
- Choosing a Poké Ball from the battle Bag is intended to return to the game's native capture screen. This flow worked in an earlier Ryujinx test build.
- EXP after a capture worked in an earlier test.
- The v8 patch restores the EXP-on-win hooks. EXP after defeating a wild Pokémon still needs confirmation with this exact build.
- The custom Options menu rows are omitted because showing them caused Ryujinx to crash.
- The v8 archive contains the IPS patch only. It does not contain game files.

The v8 build has not completed a full playthrough test. Back up your save before installing it.

## Install in Ryujinx

1. Back up your save.
2. Download `The-Better-Lets-Go-Ryujinx-v8-no-menu-exp-test.zip` from the [v8 pre-release](https://github.com/Naced28/The-Better-Lets-Go-Ryujinx/releases/tag/ryujinx-v8-test).
3. In Ryujinx, open the game's mod-management interface and add or extract the ZIP as a mod for Pokémon: Let's Go, Pikachu!.
4. Enable the mod and restart the game.

Remove other wild-battle or Better Let's Go patches for this title before testing. The patch targets only the game version and Build ID listed above.

## Source and technical notes

The patch is built from the game's own 1.0.2 executable and applies changes at fixed code addresses. Build instructions, patch layout, address information, and validation details are in [docs/TECHNICAL.md](docs/TECHNICAL.md) and [docs/RYUJINX-EXPERIMENT.md](docs/RYUJINX-EXPERIMENT.md).

Rebuilding requires your own legally obtained game files. No game executable, game assets, keys, or save data belong in this repository.

## Credits and license

- **The Better Let's Go**, the upstream project and gameplay-mod foundation: [feelingdev/The-Better-Lets-Go](https://github.com/feelingdev/The-Better-Lets-Go).
- Upstream author: [feelingdev](https://github.com/feelingdev).

This fork's changes are documented in its source and Ryujinx experiment notes. See [LICENSE](LICENSE) for the license information included with this repository. Pokémon and related marks belong to their respective owners. This is an unofficial fan project and is not affiliated with or endorsed by Nintendo, Game Freak, Creatures Inc., or The Pokémon Company.
