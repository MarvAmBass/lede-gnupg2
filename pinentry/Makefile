#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pinentry
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=ftp://ftp.gnupg.org/gcrypt/pinentry
PKG_HASH:=1672c2edc1feb036075b187c0773787b2afd0544f55025c645a71b4c2f79275a

PKG_LICENSE:=GPL-2
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=Marvin (MarvAmBass) <github.com/MarvAmBass>

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/pinentry/Default
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Encryption
  DEPENDS:=+libncurses +libreadline +libgpg-error +libassuan
  TITLE:=pinentry
  URL:=http://www.gnupg.org/
endef

define Package/pinentry
  $(call Package/pinentry/Default)
  MENU:=1
endef

define Package/pinentry/description
 pinentry program
endef


TARGET_CFLAGS += $(FPIC)

define Package/pinentry/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/pin* $(1)/usr/bin/
endef

$(eval $(call BuildPackage,pinentry))
