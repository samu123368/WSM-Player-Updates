# WSM Player updates

Open **WSM Player Settings → WSM Player Updates**. The page works with the
mouse and Wii Remote, and uses the applied theme and selected UI language.

1. Select **Check for updates**. The **Official releases** source is configured
   automatically, including migration from a previously empty saved source.
   A higher signed build ID enables installation; an equal build is up to date.
2. Select **Download and install**. Progress shows downloading and verification.
3. Select **Restart WSM Player** after installation, or reopen it later from HBC.

Public binary releases and signed manifests are published separately at
[WSM-Player-Updates](https://github.com/samu123368/WSM-Player-Updates).
The direct Wii-compatible feed is
`http://b7.185.199.108.153.nip.io/WSM-Player-Updates/update.manifest`.
The private source/backup repository stays private; no GitHub token is copied
to the Wii. No Nintendo resource packs or personal assets are published.
Custom direct HTTP or local `sd:/...` manifest sources remain supported. Clearing
the Update source field returns to the official feed, not an unconfigured state.
HTTPS, redirects, compressed and chunked responses are rejected rather than
silently using unverified TLS. Servers must send an exact Content-Length.

## What is installed

Only the application DOL beside the currently running app is replaced. This
does not install IOS, a forwarder, WADs, channels, System Menu updates, themes,
Nintendo artwork or settings packs. Existing configuration and personal assets
are not changed. Keep using the original folder when launching through a
forwarder. HBC's existing meta.xml is preserved, including its display version;
the updater itself shows the running binary's actual version/build.

Ed25519 authenticates the complete manifest with the public key in the binary.
SHA-512 verifies the downloaded DOL, including a reread from SD. Wii executable
section bounds and entry point are validated before installation. Unsigned,
altered, oversized, truncated or older/equal builds cannot be installed.
HTTP is not confidential: only public release files belong on this feed.
The signature, not HTTP or an untrusted checksum alone, authenticates updates.

Downloads run on an independent worker, leaving rendering/input polling alive.
B/Back cancels; wait until cancellation finishes before leaving the page. HOME
is temporarily unavailable while file/network operations are outstanding so
the app cannot shut down IOS or SD while its worker is active. No USB driver,
WPAD settings or runtime IOS changes are made by checking/downloading updates.

No recovery archive or old-release collection is retained. During installation
there is one temporary download and a very short rename transaction, so allow
space for approximately one extra DOL (currently ~4.5 MB). **Do not cut power
while installing.** A FAT rename transaction is not a power-loss guarantee.
If power loss leaves `boot.dol.replace`, inspect the files on a computer. When
boot.dol is missing, rename that old file back to boot.dol; when boot.dol exists,
verify it before deciding what to keep. The updater never deletes an unfinished
previous transaction automatically.

## Preparing future releases (maintainer)

The trusted public key was generated locally. The private 32-byte seed is in
`.update-signing/release.seed`. It is excluded from Git, SD packages and backup
ZIPs. **Keep a separate secure private copy**; losing it prevents signing builds
accepted by installed copies. Never upload it as a repository or release asset.
Do not rerun key initialization in a fresh checkout expecting the same identity.

1. Change `source/wsmversion.h`: version plus an increasing build ID.
2. Build/test the new DOL with the same public verification key.
3. Stage with `tools/prepare_local_asset_release.ps1`, then publish using the
   fixed allowlisted helper (requires the local signing seed and `gh` login):

   ```text
   powershell -File tools/publish_github_update.ps1
   ```

4. Verify the live deployment with `python tools/qa_update_feed.py --online`.
   GitHub Pages serves main/root from the public repository. Each DOL has an
   immutable build path; never overwrite a build with different bytes. A full
   ordinary SD ZIP is also published as a public GitHub Release asset.
5. For a custom feed, `tools/publish_update.py` generates a manifest locally
   without uploading anything. For SD testing, use a DOL URL
   such as `sd:/updates/boot.dol` and a source such as `sd:/updates/update.manifest`.

The canonical manifest is seven ordered LF-terminated lines: `WSM-UPDATE-1`,
`version=`, `build=`, `size=`, `sha512=`, `url=`, `signature=`. The first six
lines, including final LF, are signed. Hash/signature hex is lowercase. Maximum
manifest is 2 KiB; maximum DOL is 16 MiB, matching the existing app launcher.

## Dependency and verification

Monocypher 4.0.3 is vendored unmodified from
[its official project](https://github.com/LoupVaillant/Monocypher/tree/4.0.3).
It is used under its 2-clause BSD option; its notices are supplied with the
source and compiled package. [Ed25519 documentation](https://monocypher.org/manual/ed25519).

`python tools/qa_player_update.py` executes the actual production verifier and
worker using host adapters. Checks include the RFC 8032 signature vector,
Python SHA-512 interoperability, the built DOL, fragmented HTTP, cancellation,
bad signatures/hashes/executables, failed rename rollback, unchanged user files,
no retained archive, and the restart request. This does not emulate IOS, radio,
GX, a real SD card or executing the new DOL. Real-Wii online download and restart
still need hardware testing. Test fixtures never go onto the SD card.

`tools/qa_update_feed.py --online` fetches the actual public manifest and DOL
over direct HTTP without following redirects, checks headers and byte equality,
and replays those responses through the production verifier/install worker with
host adapters. It tests equal/new-build results, streaming installation, unchanged
settings/photos and restart requests. It does not execute the downloaded DOL or
prove real-Wii IOS networking/restart behavior.
