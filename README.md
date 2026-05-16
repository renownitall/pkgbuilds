# pkgbuilds

Arch Linux PKGBUILDs for packages I use that aren't available in the official repositories or the AUR.

Packages are built automatically via GitHub Actions and served as a pacman repository through GitHub Pages.

## Packages

| Package | Description |
|---|---|
| `ttf-google-sans` | Google Sans: the proportional font used across Google's branding and products |
| `ttf-google-sans-code-nerd` | Google Sans Code: the monospace variant, patched with [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts) glyphs (regular + mono) |

## Usage

Add the repository to `/etc/pacman.conf`:

```ini
[custom]
SigLevel = Optional TrustAll
Server = https://renownitall.github.io/pkgbuilds
```

Then install:

```bash
sudo pacman -Sy ttf-google-sans ttf-google-sans-code-nerd
```

## Building locally

If you'd rather build from source instead of using the hosted repository:

```bash
git clone https://github.com/renownitall/pkgbuilds.git
cd pkgbuilds/ttf-google-sans
makepkg -si
```

`ttf-google-sans-code-nerd` requires `fontforge` for Nerd Fonts patching and takes considerably longer to build:

```bash
cd pkgbuilds/ttf-google-sans-code-nerd
makepkg -si
```

## How it works

1. PKGBUILDs are pushed to `main`
2. GitHub Actions builds each package in an Arch Linux container
3. A pacman repository database is generated with `repo-add`
4. Everything is deployed to GitHub Pages

No font files are stored in this repository. They are fetched from the Google Fonts API and (for the Nerd Font variant) patched at build time.
