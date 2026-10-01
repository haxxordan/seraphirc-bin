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
- The update workflow is fully automatic: it detects new upstream releases, verifies the release checksum and GitHub asset digest, rejects unexpected dependency/layout changes, clean-builds the updated package on Arch, publishes it to the AUR, and then commits the version bump back to this repository.
- A separate AUR publish workflow keeps manual GitHub-side package changes synchronized with the AUR when `AUR_SSH_PRIVATE_KEY` is configured.

## Upstream binary dependencies

SeraphIRC 6.0.3 declares Debian dependencies corresponding to the following Arch packages:

- `gtk4`
- `webkitgtk-6.0`
- `libsecret`
- `gnome-keyring`
- `desktop-file-utils`
- `hicolor-icon-theme`
- `gst-plugins-base`
- `gst-plugins-good`
- `gst-libav`

## Security / trust model

The package downloads the official upstream release asset over HTTPS and pins its SHA-256 checksum. Automated updates also verify GitHub's release-asset SHA-256 digest, the exact expected Debian dependency set, required package layout, and a clean Arch build before anything is published.

## License

SeraphIRC's upstream license is distributed inside the binary package. This packaging repository contains only AUR packaging metadata and automation.
