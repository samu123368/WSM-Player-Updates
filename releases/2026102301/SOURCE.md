# Corresponding source — WSM Player 1.2 build 2026102301

Application source and build Makefile:
[WSM-Player revision 1c58352](https://github.com/samu123368/WSM-Player/tree/1c583529209b3e31bd78b748a91cd77374230afd).
Download a complete source ZIP from that revision's **Code → Download ZIP**
menu, or clone the repository. Full GPL v2 terms are in `COPYING.txt`.
Original permissive notices remain applicable to their components.

This release was compiled from a fresh source-only snapshot, without an
object-only patcher, Nintendo artwork or personal configuration. Build tests
and synthetic PowerPC patcher tests do not replace real-Wii verification.

External development libraries are obtained separately via devkitPro. Primary
source/build references for the toolchain and linked dependencies:

- [devkitPro toolchain build scripts](https://github.com/devkitPro/buildscripts)
  (devkitPPC r46.1, GCC 14.2.0)
- [libogc](https://github.com/devkitPro/libogc) (2.10.0, including Wii platform libraries)
- [libfat-ogc/libdvm](https://github.com/devkitPro/libdvm/tree/v2.0.1) (2.0.1,
  with [fatfs-mod 0.15.1](https://github.com/devkitPro/fatfs-mod/tree/v0.15.1))
- [Wii startup linker script](https://github.com/devkitPro/devkitppc-crtls/tree/v1.0.0)
  (devkitppc-crtls 1.0.0, `rvl.ld` matching libogc 2.10.0)
- [Wii/PowerPC portlibs build recipes](https://github.com/devkitPro/pacman-packages)
- [libgd](https://github.com/libgd/libgd) (2.3.3)
- [libjpeg-turbo](https://github.com/libjpeg-turbo/libjpeg-turbo) (3.1.4.1)
- [libpng](https://github.com/pnggroup/libpng) (1.6.55)
- [zlib](https://github.com/madler/zlib) (1.3.1)

Component notices accompany the package, including `THIRD-PARTY-NOTICES.txt`,
renderer, Monocypher and Noto notices. This software is based in part on the
work of the Independent JPEG Group. Wii resources are loaded from your own
NAND at runtime and are not distributed in the source or package.

This build uses an isolated matching r46.1 compiler and original compiled
libogc 2.10.0 / libfat-ogc 2.0.1 libraries. SDK libraries were obtained from the
official devkitpro/devkitppc:20250102 image; the Windows compiler is the archived
devkitPPC-r46.1-1-windows_x86_64 package. The source README documents selecting a
separate compatible SDK. The global SDK is not replaced. Newer-toolchain builds
1101 and 1102 failed real-Wii forwarded startup and are not validated substitutes.
