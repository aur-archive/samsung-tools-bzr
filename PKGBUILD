# Maintainer: Fortunato Ventre (voRia) <vorione AT gmail DOT com>

pkgname=samsung-tools-bzr
pkgver=563
pkgrel=1
pkgdesc="Tools for Samsung laptops - Development version"
arch=('any')
url="https://launchpad.net/samsung-tools"
license=('GPL3')
depends=('pm-utils' 'xbindkeys' 'rfkill' 'python2-dbus' 'python2-notify' 'vbetool')
makedepends=('bzr')
conflicts=('samsung-tools')
provides=('samsung-tools')
optdepends=('phc-intel: for CPU undervolting')
source=()
md5sums=()
sha1sums=()
backup=(etc/samsung-tools/system.conf
        etc/samsung-tools/session.conf
        etc/samsung-tools/scripts/bluetooth-on
        etc/samsung-tools/scripts/bluetooth-off
        etc/samsung-tools/scripts/wireless-on
        etc/samsung-tools/scripts/wireless-off)
install=samsung-tools.install

_bzrtrunk=lp:samsung-tools
_bzrmod=samsung-tools

package() {
  cd "$srcdir"

  msg "Connecting to the server...."
  if [ ! -d ./"$_bzrmod" ]; then
    bzr branch "$_bzrtrunk" "$_bzrmod"
  else
    cd "$_bzrmod"
    bzr revert
    cd ..
  fi
  msg "BZR checkout done or server timeout"

  cd "$srcdir/$_bzrmod"

  # Append bzr checkout version to version string
  sed -i "s:\(APP_VERSION = \".*\)\":\1~bzr$pkgver\":" backends/globals.py

  make DESTDIR="$pkgdir/" install || return 1

  # Use samsung-tools.install from bzr sources
  cat archlinux/samsung-tools.install > "$startdir/samsung-tools.install"
}

# vim:set ts=2 sw=2 et:
