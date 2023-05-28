m4_freebsd
==========
[![License](https://img.shields.io/badge/License-BSD_2--Clause-blue.svg)](https://opensource.org/licenses/BSD-2-Clause)
[![C89](https://img.shields.io/badge/C-89-blue)](https://en.wikipedia.org/wiki/C89_(C_version))

`m4` is one of those annoying dependencies that is used in build systems. It's also an arbitrary macro language, but that's not used as often nowadays.

Documentation: https://man.freebsd.org/cgi/man.cgi?query=m4

BSD-2-Clause: This ports their implementation from FreeBSD's source tree at [freebsd/freebsd-src@`046d8d8`](https://github.com/freebsd/freebsd-src/commit/046d8d89ed1956944b12ec4f0580c30bc202bbfb).

Anyway, this ports it from FreeBSD to Windows, Linux and others.

Specifically this adds support to:

- **Windows**

  - [coming soon] MSVC 2022* (tested on x86 and x64)
  - [coming soon] MinGW (tested on x86 and x64)
  - Cygwin

*should support all versions down to ~2010 also

- **Linux**

  - GCC
  - Clang

---

## License

Licensed under BSD 2 clause ([LICENSE-BSD-2](LICENSE-BSD) or <https://opensource.org/license/bsd-2-clause>)

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, shall be licensed as above, without any
additional terms or conditions.
