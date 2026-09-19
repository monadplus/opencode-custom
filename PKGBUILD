pkgname=opencode-custom
pkgver=1.18.31
pkgrel=3
pkgdesc="The AI coding agent built for the terminal"
arch=('x86_64' 'aarch64')
url="https://github.com/anomalyco/opencode"
license=('MIT')
depends=('ripgrep')
makedepends=('bun')
provides=('opencode')
conflicts=('opencode' 'opencode-bin')
options=('!debug' '!strip')

build() {
  cd "$startdir"
  bun install --frozen-lockfile
  OPENCODE_VERSION="$pkgver" \
    bun run --cwd packages/opencode build --single --skip-install --skip-embed-web-ui
}

package() {
  local target

  case "$CARCH" in
    x86_64)
      target='opencode-linux-x64'
      ;;
    aarch64)
      target='opencode-linux-arm64'
      ;;
  esac

  install -Dm755 \
    "$startdir/packages/opencode/dist/$target/bin/opencode" \
    "$pkgdir/usr/bin/opencode"
}
