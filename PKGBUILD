# Maintainer: CoffeeLink <aron@coffeelink.hu>
pkgname=helium-git
pkgver=0.0.1
pkgrel=1
pkgdesc="An Emulator for an arhitecture I designed out of boredom."
arch=('x86_64')
url="https://github.com/Coffeelink/helium_vm"
license=('APGL-3.0')
options=(!debug strip)
provides=('helium')
source=("helium::git+$url.git")
sha256sums=('SKIP')
depends=(
  'gcc-libs'
  'glibc'
)
makedepends=(
  'git'
  'cargo-nightly'
)

prepare() {
  mv helium/* .
  export RUSTUP_TOOLCHAIN=nightly
  cargo update
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  export RUSTUP_TOOLCHAIN=nightly
  export CARGO_TARGET_DIR=target
  cargo build --frozen --release --all-features
}

package() {
  mv target/release/helium_vm target/release/helium
  install -Dm0755 -t "$pkgdir/usr/bin/" "target/release/helium"
}
