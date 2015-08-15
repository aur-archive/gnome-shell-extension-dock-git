# Maintainer: Christian METZLER <neroth@xeked.com>
pkgname=gnome-shell-extension-dock-git
pkgver=20120809
pkgrel=1
pkgdesc="Shows a dock-style task switcher on the right side of the screen."
arch=('any')
url="http://live.gnome.org/GnomeShell/Extensions"
license=('GPL' 'LGPL')
makedepends=('git' 'gnome-common' 'intltool')
conflicts=('gnome-shell-extensions-git')
_gitroot="git://git.gnome.org/gnome-shell-extensions"
_gitname="gnome-shell-extensions"

build() {
	cd "$srcdir"
	msg "Connecting to GIT server...."

	if [ -d $_gitname ] ; then
		cd $_gitname && git pull origin
		msg "The local files are updated."
	else
		git clone $_gitroot --depth=1
	fi

	msg "GIT checkout done or server timeout"

	cd "$srcdir/$_gitname"
	./autogen.sh --prefix=/usr --enable-extensions="dock"
	make
}

package() {
	cd "$srcdir/$_gitname"
	make DESTDIR=${pkgdir} install
	rm -r ${pkgdir}/usr/share/locale
}
