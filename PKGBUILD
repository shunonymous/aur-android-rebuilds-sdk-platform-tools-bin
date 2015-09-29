# Maintainer: Vlad M. <vlad@archlinux.net>
# Contributor: Gordin <9ordin @t gmail dot com>

pkgname=android-sdk-platform-tools
pkgver=r23.0.1
pkgrel=1
pkgdesc='Platform-Tools for Google Android SDK (adb and fastboot)'
arch=('i686' 'x86_64')
url="http://developer.android.com/sdk/index.html"
license=('custom')
depends_i686=('gcc-libs' 'zlib' 'ncurses')
depends_x86_64=('lib32-gcc-libs' 'lib32-zlib' 'lib32-ncurses')
provides=('adb' 'android-tools')
conflicts=('adb')
_sdk="android-sdk"
_tools="opt/${_sdk}/tools"
_ptools="opt/${_sdk}/platform-tools"

source=("https://dl-ssl.google.com/android/repository/platform-tools_${pkgver}-linux.zip"
        "adb.service"
        "license.html")
sha256sums=('e19280af36e4753d9d4f0c6f6bdab63f36a0a025742d42cd86adb88d71fc236b'
            '1c219abea7584ae13f3f76b04e269ef21c1699d6bd29b7615523f927a9d10deb'
            'a7f3a259290ae6a5dc61bd34ecae36e2b7e2f644865ddc3c7fde5d248b8a7cef')

package() {
  install -Dm644 "${srcdir}/adb.service" "${pkgdir}/usr/lib/systemd/system/adb.service"
  install -Dm644 "${srcdir}/license.html" "usr/share/licenses/$pkgname/license.html"
  cd "$pkgdir"
  mkdir -p opt etc/profile.d
  echo 'export PATH=$PATH:/opt/android-sdk/platform-tools' > "etc/profile.d/${pkgname}.sh"
  echo 'setenv PATH ${PATH}:/opt/android-sdk/platform-tools' > "etc/profile.d/${pkgname}.csh"
  chmod 755 "etc/profile.d/${pkgname}".{csh,sh}
  mkdir -p "opt/$_sdk"
  cp -a "$srcdir/platform-tools" "$pkgdir/opt/$_sdk/platform-tools"
  chmod +Xr -R "$pkgdir/opt/$_sdk/platform-tools"
}
