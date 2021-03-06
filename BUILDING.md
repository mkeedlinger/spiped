To build and install spiped, run:

```bash
make BINDIR=/path/to/target/directory install
```

To install man pages, add `MAN1DIR=/path/to/man.1/directory` to the command
line (e.g., `MAN1DIR=/usr/local/man/man1` on FreeBSD).

Spiped should build and run on any IEEE Std 1003.1 (POSIX) compliant
system which
1. Includes the Software Development Utilities option,
2. Has OpenSSL available via `-lcrypto` and `#include <openssl/foo>`, and
3. Provides `/dev/urandom`.

On some platforms (Solaris, maybe others), additional compiler and/or linker
options are required to find OpenSSL or system libraries; these can be
provided by adding e.g., `CFLAGS="-I/path/to/openssl/headers"` (compiler option)
or `LDADD_EXTRA="-L/usr/sfw/lib -lsocket -lnsl"` (linker option) to the make
command line.

On some platforms (OpenBSD prior to 5.4, and possibly others) you will need to
add `#include <sys/types.h>` at the start of

```
lib/dnsthread/dnsthread.c
lib/util/sock_util.c
proto/proto_conn.c
spipe/main.c
spipe/pushbits.c
```
due to a POSIX-compliance bug on those platforms.

On some platforms (mostly Linuxes) it is possible to install OpenSSL libaries
wihout the associated header files; the header files are usually in packages
named "openssl-devel", "libssl-dev", or similar.

If your OS provides random bytes via some mechanism other than `/dev/urandom`,
please make local changes to `lib/util/entropy.c` and notify the author.

If spiped fails to build or run for other reasons, please notify the
author.
