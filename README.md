# Cisco syntax highlighting for Remote Desktop Manager

Colour Cisco IOS / IOS-XE configs and `show` output in **Devolutions Remote Desktop Manager (RDM)** SSH
sessions — in the colours of the [**Cisco IOS LSP**](https://github.com/Aswertus/cisco-lsp) extension for
VS Code ([Marketplace](https://marketplace.visualstudio.com/items?itemName=Aswertus.cisco-ios-lsp) ·
[Open VSX](https://open-vsx.org/extension/Aswertus/cisco-ios-lsp)), so a config looks the same in your
editor and on the live switch.

What gets coloured:

| Colour | What                                                                                                                                         |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| green  | `interface`, `description`, `vlan`, `aaa`, table headers; good state (`up`, `permit`, `connected`, `success`); `!` lines                     |
| red    | `no …`, bad state (`down`, `deny`, `shutdown`, `notconnect`, `failure`), `--More--`                                                          |
| orange | notices: `disabled`, `err-disabled`, `device-tracking` lines                                                                                 |
| purple | ACL / policy keywords (`access-group`, `route-map`, `class-map`, …) and options (`access`, `trunk`, `in`, `any`, `match-all`, `portfast`, …) |
| teal   | protocols (`ssh`, `tcp`, `bgp`, `ospf`, `vrf`, …), `authentication`/`authorization`/`accounting`, whole `snmp-server` lines                  |
| yellow | interfaces (`GigabitEthernet1/0/1`, `Vlan10`, `Po1`, `LISP0.100`, …), `line con/vty`, `address-family`                                       |
| white  | your values: IPv4/IPv6/MAC addresses, host/ACL/VRF/class-map names, secrets                                                                  |
| plain  | banner art and everything else                                                                                                               |

## Two sets

| Folder                                      | For a terminal with                   | Files                                                              |
| ------------------------------------------- | ------------------------------------- | ------------------------------------------------------------------ |
| [`default-background/`](default-background) | RDM's default black background        | `RDM-Cisco-Vivid.xml`                                              |
| [`vscode-background/`](vscode-background)   | VS Code's dark background (`#232425`) | `RDM-Cisco-Vivid.xml` + `Daybreak-RDM-Dark.txt` (terminal colours) |

Each rule's background equals its set's terminal background, so pick the set that matches your terminal —
the wrong one shows boxes behind coloured words.

Download the folders from the [latest release](../../releases/latest) (zip) or straight from this repository.

## Install

Tested with RDM 2026.3 (Windows).

1. _vscode-background only:_ **File → Settings → Types → Terminal → Colors** → _Override mode:_ **Override** →
   **Import** → `Daybreak-RDM-Dark.txt`. (Export your current colours first if you may want to go back.)
2. **File → Settings → Types → Terminal → Syntax highlighting** → **create a profile** (e.g. `Cisco`).
3. Inside that profile's rule list: **Import** → `RDM-Cisco-Vivid.xml` → **Save**.
4. Choose the profile on your SSH entries (**Terminal → Display**), connect, `show running-config`.

Notes:

- **Import adds rules below the existing ones.** Importing into a profile that already has rules leaves the old
  ones on top, and they win. Import into an empty profile.
- Import inside the **profile's rule list**. On the profiles list RDM answers
  `<SyntaxHighlightingItemList> was not expected`.
- RDM colours one line at a time, so banner lines are recognised by their first character (`|`, `+`, `*`, …).
  A banner line starting with a letter is coloured like config.

## Credits

The rule set started from [alalexiev's Cisco IOS / IOS-XE / IOS-XR highlighting profile](https://forum.devolutions.net/topics/35196)
on the Devolutions forum (2021). Its word lists were repaired (whole-word matching, no whole-line matches,
interface names that need a number) and extended with the VS Code extension's keyword set.

Not affiliated with Devolutions or Cisco. _Remote Desktop Manager_ is a product of Devolutions Inc.;
_Cisco_ and _IOS_ are trademarks of Cisco Systems, Inc.

## License

[MIT](LICENSE)
