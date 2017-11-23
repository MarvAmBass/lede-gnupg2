#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gnupg
PKG_VERSION:=2.2.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=ftp://ftp.gnupg.org/gcrypt/gnupg
PKG_HASH:=bfb62c7412ceb3b9422c6c7134a34ff01a560f98eb981c2d96829c1517c08197

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=Marvin (MarvAmBass) <github.com/MarvAmBass>

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/gnupg/Default
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Encryption
  DEPENDS:=+zlib +libncurses +libreadline +libpcsclite +libusb-1.0 +libgnutls +libcurl +libassuan +libgcrypt +libgpg-error +libksba +npth +ccid #+ntbtls #+libusb-compat
  TITLE:=GNU privacy guard - a free PGP replacement
  URL:=http://www.gnupg.org/
endef

define Package/gnupg
  $(call Package/gnupg/Default)
  MENU:=1
endef

define Package/gnupg/description
 GnuPG is GNU's tool for secure communication and data storage.
 It can be used to encrypt data and to create digital signatures.
 It includes an advanced key management facility and is compliant
 with the proposed OpenPGP Internet standard as described in RFC2440.
 .
 GnuPG does not use any patented algorithms so it cannot be compatible
 with PGP2 because it uses IDEA (which is patented worldwide).
endef

TARGET_CFLAGS += $(FPIC)

define Package/gnupg/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/gpg* $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/scdaemon $(1)/usr/lib/
endef

$(eval $(call BuildPackage,gnupg))
