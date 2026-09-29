# omarchy-terminal

Omarchy's terminal and the command-line tools its shipped shell configuration and
desktop entries actually consume, as a charly layer.

The `omarchy-terminal` candy installs `foot` — the terminal Omarchy's Hyprland
bindings and `xdg-terminal-exec` launch — plus `starship`, whose init the shipped
rc sources, and the modern coreutils that rc names (`bat`, `eza`, `fzf`,
`zoxide`, `dua-cli`). It also installs `fd`, `ripgrep`, `tldr`, `inxi`,
`qrencode` and `zbar` for parity with Omarchy's base package list, and the
Omarchy-published TUIs `herdr` and `cliamp`.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `omarchy-terminal` |
| Requires | `layer-omarchy-base` (the foundation layer) |
| Terminal | `foot` |
| Prompt | `starship`, `bash-completion` |
| Coreutils | `bat`, `eza`, `fzf`, `zoxide`, `dua-cli` |
| Parity set | `fd`, `ripgrep`, `tldr`, `inxi`, `qrencode`, `zbar` |
| Omarchy TUIs | `herdr`, `cliamp`, `btop` |
| Service / port | none |

## Things worth knowing

`bat` is load-bearing: the shipped `envs` exports
`MANPAGER="sh -c 'col -bx | bat -l man -p'"` **unguarded**, so without `bat`
every `man` invocation breaks. The other rc references (`eza`, `fzf`, `zoxide`)
are `command -v`-guarded, so a missing binary degrades silently — the alias or
key-binding simply never gets defined.

## How to use it

Compose the layer by pinning the member candy's sub-path in a desktop box's
`candy:` list:

```yaml
my-omarchy-desktop:
  candy:
    base: omarchy
    candy:
      - '@github.com/opencharly/layer-omarchy-base/candy/omarchy-base:v2026.242.0701'
      - '@github.com/opencharly/layer-omarchy-terminal/candy/omarchy-terminal:v2026.242.0616'
```

## Layout

- `charly.yml` — repo shape: the `discover:` rule that finds the member candy.
- `candy/omarchy-terminal/charly.yml` — the candy entity (the `distro:` package
  arm and the `plan:` `check:` assertions).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Closest family skill: `/charly-distros:omarchy-base` — the nearest owning procedure; this
  repo carries no `skill:` entity of its own.
- Foundation: `/charly-distros:omarchy-base`.
- Shell: `/charly-distros:omarchy-shell`.
- [`opencharly/opencharly](https://github.com/opencharly/opencharly) — the umbrella.
