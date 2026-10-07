# WSM Player updates

Official signed binary updates for **WSM Player**, by Dimok, Giantpune and samu.
This repository contains public builds and signed manifests only, not private
source snapshots, personal settings, logs, backups or Nintendo resource packs.
WSM Player reads the required Wii UI resources locally from the console's NAND.
It is an unofficial homebrew application, not a Nintendo product.

In the current app, open **WSM Player Settings → WSM Player Updates → Check for
updates**. The official feed is configured automatically. A newer build enables
**Download and install**, followed by **Restart WSM Player**. An equal build
reports that you are up to date. Keep power on throughout installation.

For a manual installation, download the `WSM-Player-<build>.zip` from
[Releases](https://github.com/samu123368/WSM-Player-Updates/releases) and extract
the `apps/wsmplayer` folder onto the SD card. Existing personal settings are not
included in the ZIP. Existing builds without the official feed need this manual
installation once, or the manifest URL below entered in their update settings.

The Wii-compatible, public feed is:
`http://b7.185.199.108.153.nip.io/WSM-Player-Updates/update.manifest`.
It uses Ed25519-signed manifests and SHA-512-verified DOLs. HTTP is not private;
only public files belong here. Authenticity depends on the verification key
compiled into WSM Player, not on trusting HTTP or a plain checksum.

Updates replace only WSM Player's `boot.dol`. They do not install IOS, WADs,
forwarders, themes or NAND content. No recovery archives are retained on SD.
The updater displays the running binary's version/build; HBC's existing
`meta.xml` is preserved during an in-app update.

Each build has an immutable `releases/<build>/boot.dol` path. The root signed
manifest points to the latest published build. The signing seed is never
uploaded. The original renderer software notice, Monocypher notices and Noto
font notices accompany each downloadable package. This is not a declaration
that every legacy dependency has received a complete licensing audit.
