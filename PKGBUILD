# Maintainer: Soymadip <soumadip@zohomail.in>

pkgname=ireader-bin
pkgver=2.0.13
pkgrel=1
pkgdesc="Open source novel reader for Android & Desktop"
arch=('x86_64')
_repo="IReaderorg/IReader"
url="https://github.com/${_repo}"
license=('Apache-2.0')
depends=('glibc' 'fuse2')
optdepends=('xdg-utils: desktop integration support')
provides=('ireader')
conflicts=('ireader')
options=('!strip')

_appimage="IReader-x86_64.AppImage"

source=(
  "${url}/releases/download/v${pkgver}/${_appimage}"
  "LICENSE::https://raw.githubusercontent.com/${_repo}/master/LICENSE"
)

sha256sums=('SKIP' 'SKIP')

prepare() {
  cd "$srcdir"
  chmod +x "${_appimage}"
  "./${_appimage}" --appimage-extract >/dev/null
}

package() {
  cd "$srcdir/squashfs-root"

  # Install main binary wrapper
  install -Dm755 usr/bin/ireader \
    "$pkgdir/usr/bin/ireader"

  # Install jar file
  install -Dm644 usr/bin/IReader.jar \
    "$pkgdir/usr/lib/ireader/IReader.jar"

  # Install desktop file
  install -Dm644 usr/share/applications/ireader.desktop \
    "$pkgdir/usr/share/applications/ireader.desktop"

  # Install icons
  cp -r usr/share/icons "$pkgdir/usr/share/"

  # Install top-level icon fallback
  install -Dm644 "$srcdir/squashfs-root/ireader.png" \
    "$pkgdir/usr/share/icons/hicolor/512x512/apps/ireader.png"

  # Install license
  install -Dm644 "$srcdir/LICENSE" \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
