#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libassuan
PKG_VERSION:=2.4.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://www.gnupg.org/ftp/gcrypt/libassuan/
PKG_HASH:=22843a3bdb256f59be49842abf24da76700354293a066d82ade8134bb5aa2b71

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=Marvin (MarvAmBass) <github.com/MarvAmBass>

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libassuan/Default
  SECTION:=gnupg2
  CATEGORY:=GnuPG2
  SUBMENU:=Encryption
  DEPENDS:=+libgpg-error
  TITLE:=Libassuan is the IPC library used by some GnuPG related software.
  URL:=http://www.gnupg.org/
endef

define Package/libassuan
  $(call Package/libassuan/Default)
  MENU:=1
endef

define Package/libassuan/description
 Libassuan is a small library implementing the so-called Assuan protocol. This protocol is used for IPC between most newer GnuPG components. Both, server and client side functions are provided.

 In an ideal world, Assuan is irrelevant. Assuan's primary use is to allow a client to interact with a non-persistent server. Using Assuan, this is accomplished by forking a subprocess and communicating with it via, for example, a pipe or unix domain socket. This method is neither elegant nor efficient especially when there is a lot of data spread across several transactions: not only is there a penalty for an increased number of context switches, but also a significant amount of data is memcpy-ed from the client to a file descriptor and from the file descriptor to the server. Despite these and other disadvantages, this type of client/server communication can be useful: the client is completely separate from the server; they are in different address spaces. This is especially important in situations where the server must have a known degree of reliability and data must be protected: as the Assuan protocol is well defined and clients cannot corrupt the servers' address space, auditing become much easier.

 Assuan was developed for use by the GNU Privacy Guard, GnuPG, to prevent potentially buggy clients from unwittingly corrupting sensitive transactions or compromising data such as a secret key. Assuan permits the servers, which do the actual work, e.g. encryption and decryption of data using a secret key, to be developed independently of the user interfaces, e.g. mail clients and other encryption front ends. Like a shared library, the interface is well defined and any number of front ends can use it; however, unlike a shared library, the client cannot see or touch the server's data. As with any modular system, Assuan helps keep the servers small and understandable, and helps to make code more understandable and less error prone.

 Assuan is not, however, limited to use with GnuPG servers and clients: it was design to be flexible enough to meet the demands of almost any transaction based environment with non-persistent servers.
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
  --enable-shared \
	--enable-static

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/bin $(2)/bin $(1)/usr/include $(1)/usr/lib $(1)/usr/share/aclocal
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/libassuan-config $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/assuan*.h $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libassuan.{la,a,so*} $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/aclocal/libassuan.m4 $(1)/usr/share/aclocal/
	$(SED) 's,^libdir=\"$$$${exec_prefix}/lib,libdir=\"$(STAGING_DIR)/usr/lib,g' $(1)/usr/bin/libassuan-config
	$(SED) 's,^includedir=\"$$$${prefix}/include/,includedir=\"$(STAGING_DIR)/usr/include/,g' $(1)/usr/bin/libassuan-config
	ln -sf $(STAGING_DIR)/usr/bin/libassuan-config $(2)/bin/
endef

define Package/libassuan/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libassuan.so.* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,libassuan))
