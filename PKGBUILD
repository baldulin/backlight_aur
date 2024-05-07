arch=('any')
url='https://github.com/baldulin/backlight'
license=('MIT')
pkgver=0.0.3
pkgrel=1
pkgname='python-backlight'
_name=backlight
makedepends=(python-build python-installer python-wheel)
source=("https://github.com/baldulin/backlight/archive/refs/tags/$pkgver.tar.gz")
sha512sums=(57fb29790d20de60d2f640acdfdae4a7947e79cbf563c6a2cbac620969e1109b6f9f578e75c7794b91ea8fbe63d6c33f7f92e669d2653f2cef4ef9d67dfa95f0)

build() {
    cd "$_name-$pkgver/"
    python -m build --wheel --no-isolation
}

package() {
    cd "$_name-$pkgver"
    python -m installer --destdir="$pkgdir" dist/backlight-$pkgver-py3-*.whl

    cat > "$srcdir/90-light-backlight.rules" <<EOT
ACTION=="add", SUBSYSTEM=="backlight", RUN+="/bin/chgrp video /sys/class/backlight/%k/brightness"
ACTION=="add", SUBSYSTEM=="backlight", RUN+="/bin/chmod g+w /sys/class/backlight/%k/brightness"
EOT
    install -d "$pkgdir/usr/lib/udev/rules.d/"
    install "$srcdir/90-light-backlight.rules" "$pkgdir/usr/lib/udev/rules.d/"
}
