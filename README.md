# seraphirc-bin

Arch Linux / AUR packaging for [SeraphIRC](https://www.seraphirc.chat/), a modern desktop IRC client built with Go and Wails.

This repository repackages the official upstream Debian binary published by [seraphirc/seraphirc-download](https://github.com/seraphirc/seraphirc-download). It does not build SeraphIRC from source.

## Install

Once published to the AUR:

```bash
yay -S seraphirc-bin
```

Or build locally:

```bash
git clone https://github.com/haxxordan/seraphirc-bin.git
cd seraphirc-bin
makepkg -si
```

## Maintenance

- `PKGBUILD` is the source of truth.
- `.SRCINFO` is regenerated with `makepkg --printsrcinfo > .SRCINFO`.
- `.nvchecker.toml` tracks upstream GitHub releases.
- GitHub Actions checks the package in a clean Arch container.
- The update workflow proposes version bumps when upstream publishes a new release.
- A separate AUR publish workflow can push approved package metadata to the AUR when `AUR_SSH_PRIVATE_KEY` is configured.

## Upstream binary dependencies

SeraphIRC 6.0.1 declares Debian dependencies corresponding to the following Arch packages:

- `gtk3`
- `webkit2gtk-4.1`
- `libsecret`
- `gnome-keyring`
- `desktop-file-utils`
- `hicolor-icon-theme`
- `gst-plugins-base`
- `gst-plugins-good`
- `gst-libav`

## Security / trust model

The package downloads the official upstream release asset over HTTPS and pins its SHA-256 checksum. CI also verifies expected package layout before accepting updates.

## License

SeraphIRC's upstream license is distributed inside the binary package. This packaging repository contains only AUR packaging metadata and automation.
