# ruff-debian

> Fork of [dariogriffo/ruff-debian](https://github.com/dariogriffo/ruff-debian) (MIT); the original packaging is by Dario Griffo. Served at [deb.gaofn.xyz](https://deb.gaofn.xyz) for Debian 12 (bookworm) and 13 (trixie).

Debian and Ubuntu packaging for [Ruff](https://docs.astral.sh/ruff/) — an
extremely fast Python linter and code formatter, written in Rust by Astral.

Packages are built automatically from official upstream releases (usually
within hours) and served from **[deb.gaofn.xyz](https://deb.gaofn.xyz)** for
Debian (bookworm, trixie, forky, sid) and Ubuntu (jammy, noble, questing,
resolute) on amd64, arm64, armel, armhf, ppc64el, s390x, riscv64 and i386.

## Install

```bash
sudo install -d -m 0755 /etc/apt/keyrings
sudo curl -fsSL https://deb.gaofn.xyz/deb.gaofn.xyz.gpg -o /etc/apt/keyrings/deb.gaofn.xyz.gpg
sudo curl -fsSL https://deb.gaofn.xyz/deb.gaofn.xyz.sources -o /etc/apt/sources.list.d/deb.gaofn.xyz.sources
# Debian 12 (bookworm): fetch deb.gaofn.xyz-bookworm.sources instead
sudo apt update
sudo apt install -y ruff
```

### Manual Installation

1. Download the .deb package for your Debian version available on
   the [Releases](https://github.com/gaofengnan/ruff-debian/releases) page.
2. Install the downloaded .deb package.

```sh
sudo dpkg -i <filename>.deb
```

## How it works

- `check-upstream.yml` polls upstream hourly; a new release dispatches `release.yml`.
- `release.yml` builds binary packages (Docker, per suite × architecture, from the
  upstream musl/gnu tarballs) and source packages (`.dsc`), then publishes a GitHub
  release tagged `<version>+<build>`.
- The deb.gaofn.xyz mirror ingests published releases automatically.

Manual build: `./build.sh <version> <build> [arch|all]` (e.g. `./build.sh 0.15.21 1 all`).

## Links

- Upstream: https://github.com/astral-sh/ruff
- Repository: https://deb.gaofn.xyz
