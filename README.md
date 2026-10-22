# Kumiko package repositories

Signed APT and RPM repositories for [Kumiko](https://github.com/iqzer0/kumiko),
served from <https://iqzer0.github.io/kumiko-packages/>. Add one once and
Kumiko updates with the rest of your system.

## Ubuntu, Debian, Linux Mint, Pop!_OS

```bash
sudo curl -fsSLo /usr/share/keyrings/kumiko.gpg https://iqzer0.github.io/kumiko-packages/kumiko.gpg
sudo curl -fsSLo /etc/apt/sources.list.d/kumiko.sources https://iqzer0.github.io/kumiko-packages/apt/kumiko.sources
sudo apt update && sudo apt install kumiko
```

## Fedora

```bash
sudo curl -fsSLo /etc/yum.repos.d/kumiko.repo https://iqzer0.github.io/kumiko-packages/rpm/kumiko.repo
sudo dnf install kumiko
```

## openSUSE Tumbleweed and Leap

```bash
sudo zypper addrepo https://iqzer0.github.io/kumiko-packages/rpm/kumiko.repo
sudo zypper refresh      # asks you to trust the Kumiko key: check the fingerprint below
sudo zypper install kumiko
```

## Arch Linux, Manjaro, EndeavourOS

Use the AUR: `kumiko-bin` (the release build) or `kumiko` (built from source).

## Trusting the key

The repositories are signed with the Kumiko repository key; dnf and zypper ask
you to trust it on first use. Accept it only if the fingerprint is

    D5D9 7A22 F23B 9986 B0FC  F84E ED24 5861 5AA0 8E7B

(also in Kumiko's [install guide](https://github.com/iqzer0/kumiko/blob/master/docs/install.md)
and in `repo-key.fingerprint` here, which the publishing workflow enforces).

## How this repository works

There are no packages in this git repository. The *Publish package
repositories* workflow rebuilds both repositories from Kumiko's published
releases every 6 hours (or on demand from the Actions tab), checks each
release's `SHA256SUMS.asc` against the maintainer keys in `maintainers.asc`,
signs the result with the `REPO_SIGNING_KEY` secret and deploys it to GitHub
Pages. The scripts it runs live in Kumiko's `packaging/repo`.
