# Naviamp Flatpak distribution

Official signed Linux x86_64 packages of [Naviamp](https://github.com/goosepod/naviamp).
The first package contains the existing public application v2.10.0. Packaging revisions do not
change its application version or replace its original release artifacts.

The stable installer is published at
<https://goosepod.com/naviamp-flatpak/Naviamp.flatpakref>. Publication is complete only after the
workflow has deployed and verified the signed remote and made its distribution release public.

```sh
flatpak install --user --from https://goosepod.com/naviamp-flatpak/Naviamp.flatpakref
flatpak run io.github.goosepod.Naviamp
flatpak update --user io.github.goosepod.Naviamp
```

The installer adds Naviamp's stable update remote and offers the Freedesktop runtime from Flathub.
Java is included. Linux x86_64 and X11/XWayland are supported. Other architectures and native
Wayland are not claimed. Existing DEB/RPM/ZIP installations keep their own data; use Naviamp's
settings export/import for an intentional migration. Flatpak does not silently import credentials.

## Maintainers

Source manifests, preparation, verification and native sandbox tests live in
[Naviamp's packaging directory](https://github.com/goosepod/naviamp/tree/main/packaging/flatpak).
Build and sign locally with the pinned identity; the private key stays on the maintainer's computer.
This repository receives only public signed files and needs no signing secret.

1. Prepare the signed output using Naviamp's documented `prepare.py` and `publish.py` commands.
2. Create a draft release tagged `vX.Y.Z-flatpak.N`, named exactly `Naviamp vX.Y.Z`.
3. Upload the generated public asset directory, including `SHA256SUMS`, `source.json`, installer,
   key, bundle, repository archive and `pages.tar.zst`. Never upload a private signing home or profile.
4. Dispatch **Publish Flatpak** with that distribution tag. It verifies accepted source and the
   pinned public identity, tests native playback and UI, deploys Pages, checks HTTPS and signatures,
   then publishes the release. A failed draft remains private and must be investigated.

The stable remote is <https://goosepod.com/naviamp-flatpak/repo/>. Never bypass GPG verification.
Public signing fingerprint: `47DCCEF27F4F56B168350BB3DB9D51B285362245`.
Retain the same identity and repository history for updates, keep an encrypted offline backup of
the local secret key and revocation certificate, and plan rotation before its expiry.

Pages deployment uses this repository's separate project site; it does not replace the Goosepod
website. Publication is limited to 900 MiB, including retained history and static deltas. GitHub
Releases retain immutable public bundles and repository archives for recovery and later builds.

Tracking: [Naviamp #292](https://github.com/goosepod/naviamp/issues/292).
