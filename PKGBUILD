# Maintainer: artist for Sonic-DE

pkgbase=sonic-workspace
pkgname=(sonic-workspace sonic-x11-session)
pkgver=6.6.3
_pkgver="${pkgver}"
pkgrel=5
pkgdesc='Various components needed to run a Sonic-DE-based environment. Including fixes and improvements for X11 sessions'
arch=(x86_64)
url='https://github.com/Sonic-DE/sonic-workspace'
license=(LGPL-2.0-or-later)
depends=(accountsservice
         appstream-qt
         dbus
         fontconfig
         freetype2
         gcc-libs
         glibc
         icu
         kactivitymanagerd
         karchive
         kauth
         kbookmarks
         kcmutils
         kcolorscheme
         kcompletion
         kconfig
         kconfigwidgets
         kcoreaddons
         kcrash
         kde-cli-tools
         kdeclarative
         kded
         kdbusaddons
         kguiaddons
         kholidays
         ki18n
         kiconthemes
         kidletime
         kio
         kio-extras
         kio-fuse
         kirigami
         kirigami-addons
         kitemmodels
         kjobwidgets
         knewstuff
         knighttime
         knotifications
         knotifyconfig
         kpackage
         kparts
         kpipewire
         krunner
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
         kwindowsystem
         kxmlgui
         libcanberra
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
         #milou
         ocean-sound-theme
         plasma-activities
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
         sonic-frameworks-keybind
         sonic-interface-libraries
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
             extra-cmake-modules
             git
             kdoctools
             dbus
             networkmanager-qt
             phonon-qt6
             qcoro)
groups=(sonicde)
source=("$pkgname-${_pkgver}.tar.gz::${url}/archive/refs/tags/${_pkgver}.tar.gz")
#source=("git+${url}.git#tag=$_pkgver")
sha256sums=('15fbcbcf649020be073d9a9ab77d459d8fea720ffe11aeeb7a7fe34188d60615')

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
  groups=(sonicde)

  install -Dm644 build/login-sessions/plasmax11.desktop -t "$pkgdir"/usr/share/xsessions
}

