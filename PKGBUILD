# Maintainer: callmetango
# Contributor: artist <artist@artixlinux.org>

pkgbase=sonic-workspace
pkgname=(sonic-workspace sonic-x11-session)
pkgver=6.6.5.1
_pkgver="${pkgver}"
pkgrel=1
pkgdesc='Various components needed to run a Sonic-DE-based environment. Including fixes and improvements for X11 sessions'
arch=(x86_64)
url='https://github.com/Sonic-DE/sonic-workspace'
license=(LGPL-2.0-or-later)
depends=(accountsservice
         appstream-qt
         elogind
         fontconfig
         freetype2
         glibc
         icu
         kactivitymanagerd
         karchive
         kbookmarks
         kcmutils
         kcolorscheme
         kcompletion
         kconfig
         kconfigwidgets
         kcrash
         kde-cli-tools
         kdeclarative
         kded
         kdbusaddons
         kholidays
         ki18n
         kiconthemes
         kidletime
         kio-fuse
         kitemmodels
         kjobwidgets
         knewstuff
         knotifications
         knotifyconfig
         kpackage
         kparts
         kpipewire
         kquickcharts
         kservice
         kstatusnotifieritem
         ksvg
         ksystemstats
         ktexteditor
         ktextwidgets
         kuserfeedback
         kwallet
         kwidgetsaddons
         kxmlgui
         libcanberra
         libgcc
         libice
         libkexiv2
         libqalculate
         libsm
         libx11
         libxau
         libxcb
         libxcrypt
         libxcursor
         libxfixes
         libxft
         libxtst
         milou
         ocean-sound-theme
         plasma-activities-stats
         plasma5support
         prison
         qt6-5compat
         qt6-base
         qt6-declarative
         qt6-location
         qt6-positioning
         qt6-svg
         qt6-tools # for qdbus
         qt6-virtualkeyboard
         sh
         solid
         sonic-activities
         sonic-frameworks-auth
         sonic-frameworks-core-addons
         sonic-frameworks-gui-addons
         sonic-frameworks-io
         sonic-frameworks-io-extras
         sonic-frameworks-keybind
         sonic-frameworks-quick-ui
         sonic-frameworks-runner
         sonic-frameworks-windowsystem
         sonic-interface-libraries
         sonic-night-light
         sonic-screenlocker
         sonic-sysguard-library
         sonic-win
         xcb-util
         xcb-util-cursor
         xcb-util-image
         xorg-xmessage
         xorg-xrdb
         zlib)
makedepends=(baloo
             git
             libelogind
             networkmanager-qt
             phonon-qt6
             qcoro
             sonic-frameworks-cmake-modules
             sonic-frameworks-doctools)
groups=(sonicde)
source=("$pkgname-$pkgver.tar.gz::${url}/archive/refs/tags/${pkgver}.tar.gz")
sha256sums=('84182ea3367b1645cf2b772df44a5f0155776bd951856eb218a09980db343e55')

build() {
  cmake -B build -S $pkgname-$_pkgver \
    -DCMAKE_INSTALL_LIBEXECDIR=lib \
    -DGLIBC_LOCALE_GEN=OFF \
    -DBUILD_TESTING=OFF
  cmake --build build
}

package_sonic-workspace() {
  optdepends=('appmenu-gtk-module: global menu support for some GTK3 applications'
            'baloo: Baloo search runner'
            'discover: manage applications installation from the launcher'
            'kdepim-addons: displaying PIM events in the calendar'
            'networkmanager-qt: IP based geolocation'
            'sonic-workspace-wallpapers: additional wallpapers'
            'plasma5-integration: use Plasma settings in Qt5 applications'
            'xdg-desktop-portal-gtk: sync font settings to Flatpak apps')
  depends+=(sonic-x11-session plasma-integration) # Declare runtime dependency here to avoid dependency cycles at build time
  conflicts=(plasma-workspace plasma-wayland-session)
  provides=(plasma-workspace)
  replaces=(plasma-workspace)
  groups=(sonicde)

  DESTDIR="$pkgdir" cmake --install build

  rm -r "$pkgdir"/usr/share/xsessions/plasmax11.desktop

  rm -r $pkgdir/usr/lib/systemd
}

package_sonic-x11-session() {
  pkgdesc='Plasma X11 session, sonic edition, for XLibre'
  depends=(sonic-workspace)
  provides=(plasma-x11-session)
  conflicts=(plasma-x11-session)
  replaces=(plasma-x11-session)
  groups=(sonicde)

  install -Dm644 build/login-sessions/plasmax11.desktop -t "$pkgdir"/usr/share/xsessions
  sed -i 's|Plasma (X11)|SonicDE|' "$pkgdir"/usr/share/xsessions/plasmax11.desktop
}
