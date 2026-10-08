# Corresponding source — WSM Player 1.2 build 2026100901

Application source and build Makefile:
[WSM-Player revision 0469dbd](https://github.com/samu123368/WSM-Player/tree/0469dbdcb3a7eed85b0cc4b8175bec174e1fae16).
Download a complete source ZIP from that revision's **Code → Download ZIP**
menu, or clone the repository. Full GPL v2 terms are in `COPYING.txt`.
Original permissive notices remain applicable to their components.

This release was compiled from a fresh source-only snapshot, without an
object-only patcher, Nintendo artwork or personal configuration. Build tests
and synthetic PowerPC patcher tests do not replace real-Wii verification.

External development libraries are obtained separately via devkitPro. Primary
source/build references for the toolchain and linked dependencies:

- [devkitPro toolchain build scripts](https://github.com/devkitPro/buildscripts)
  (devkitPPC r46.1)
- [libogc](https://github.com/devkitPro/libogc) (2.10.0, including Wii platform libraries)
- [libfat](https://github.com/devkitPro/libfat) (2.0.1)
- [Wii/PowerPC portlibs build recipes](https://github.com/devkitPro/pacman-packages)
- [libgd](https://github.com/libgd/libgd) (2.3.3)
- [libjpeg-turbo](https://github.com/libjpeg-turbo/libjpeg-turbo) (3.1.4.1)
- [libpng](https://github.com/pnggroup/libpng) (1.6.55)
- [zlib](https://github.com/madler/zlib) (1.3.1)

Component notices accompany the package, including `THIRD-PARTY-NOTICES.txt`,
renderer, Monocypher and Noto notices. This software is based in part on the
work of the Independent JPEG Group. Wii resources are loaded from your own
NAND at runtime and are not distributed in the source or package.
