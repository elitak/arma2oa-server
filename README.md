See [debian/README.Debian.md](debian/README.Debian.md) for most of the packaging notes.

### Building:

* `tar xaf a2oa-server-1.60.94743.tar.bz2`, or whichever version of the
  upstream tarball you want to include in the package.
* Edit debian/changelog to set version appropriately
* `dpkg-buildpackage -uc -b`
