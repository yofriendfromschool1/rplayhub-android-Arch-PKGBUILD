# Maintainer: yofriendfromschool1
pkgname=rplayhub-android-bin
pkgver=1.0.1
pkgrel=1
pkgdesc="Mirror and control Android phones on Linux (binary repackage)"
arch=('x86_64')
url="https://github.com/rPlayAI/rplayhub-android"
license=('Apache-2.0')
depends=('sdl2' 'ffmpeg' 'adb' 'zlib' 'openssl')
source=("${pkgname}-${pkgver}.deb::https://github.com/rPlayAI/rplayhub-android/releases/download/linux-v${pkgver}/rplayhub-android_${pkgver}-1_amd64.deb")
sha256sums=('1802aa5be479a375b5c10899222aca34ea335d06e783b8078a3d05185b71137a')

package() {
    # Extract the .deb (an ar archive) into a temp directory
    bsdtar -xf "$srcdir/${pkgname}-${pkgver}.deb" -C "$srcdir"
    
    # The actual filesystem contents are inside data.tar.*
    local data_tar=$(find "$srcdir" -maxdepth 1 -name 'data.tar.*' -type f | head -n1)
    if [ -z "$data_tar" ]; then
        error "data.tar not found in .deb"
    fi
    
    # Extract the data archive directly into $pkgdir
    bsdtar -xf "$data_tar" -C "$pkgdir"
    
    # Clean up the extracted archive files
    rm -f "$srcdir"/data.tar.* "$srcdir"/control.tar.* "$srcdir"/debian-binary
}
