#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=npth
PKG_VERSION:=1.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://www.gnupg.org/ftp/gcrypt/npth/
PKG_HASH:=294a690c1f537b92ed829d867bee537e46be93fbd60b16c04630fbbfcd9db3c2

PKG_LICENSE:=GPL-2.1
PKG_LICENSE_FILES:=COPYING.LIB
PKG_MAINTAINER:=Marvin (MarvAmBass) <github.com/MarvAmBass>

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/npth/Default
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Encryption
  DEPENDS:=+libgpg-error
  TITLE:=npth The New GNU Portable Threads Library.
  URL:=http://www.gnupg.org/
endef

define Package/npth
  $(call Package/npth/Default)
  MENU:=1
endef

define Package/npth/description
 nPth is a library to provide the GNU Pth API and thus a non-preemptive threads implementation.

 In contrast to GNU Pth is is based on the system's standard threads implementation. This allows the use of libraries which are not compatible to GNU Pth. Experience with a Windows Pth emulation showed that this is a solid way to provide a co-routine based framework.
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
  --enable-shared \
	--enable-static

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/bin $(2)/bin $(1)/usr/include $(1)/usr/lib $(1)/usr/share/aclocal
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/npth-config $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/npth*.h $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libnpth.{la,a,so*} $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/aclocal/npth.m4 $(1)/usr/share/aclocal/
	$(SED) 's,^libdir=\"$$$${exec_prefix}/lib,libdir=\"$(STAGING_DIR)/usr/lib,g' $(1)/usr/bin/npth-config
	$(SED) 's,^includedir=\"$$$${prefix}/include/,includedir=\"$(STAGING_DIR)/usr/include/,g' $(1)/usr/bin/npth-config
	ln -sf $(STAGING_DIR)/usr/bin/npth-config $(2)/bin/
endef

define Package/npth/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libnpth.so.* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,npth))
