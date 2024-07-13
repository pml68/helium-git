# Maintainer: CoffeeLink <aron@coffeelink.hu>
pkgname=helium-git
pkgver=0.4.5.g1bf81a0
pkgrel=1
pkgdesc="An Emulator for an arhitecture I designed out of boredom."
arch=('x86_64')
url="https://github.com/Coffeelink/helium_vm"
license=('AGPL-3.0-or-later')
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

pkgver() {
  echo "$(cargo metadata --format-version 1  | jq -r '.packages[]  | select(.name | test("helium_vm")) | .version').g$(git rev-parse --short HEAD)"
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
