#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libksba
PKG_VERSION:=1.3.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://www.gnupg.org/ftp/gcrypt/libksba/
PKG_HASH:=41444fd7a6ff73a79ad9728f985e71c9ba8cd3e5e53358e70d5f066d35c1a340

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=Marvin (MarvAmBass) <github.com/MarvAmBass>

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libksba/Default
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Encryption
  DEPENDS:=+libgpg-error #+libncurses +libreadline +libpcsclite +libusb-compat
  TITLE:=Libksba provides an easy API to create and parse X.509 and CMS related objects.
  URL:=http://www.gnupg.org/
endef

define Package/libksba
  $(call Package/libksba/Default)
  MENU:=1
endef

define Package/libksba/description
 Libksba is a library to make the tasks of working with X.509 certificates, CMS data and related objects more easy. It provides a highlevel interface to the implemented protocols and presents the data in a consistent way. There is no more need to worry about all the nasty details of the protocols. The API gives the C programmer an easy way of interacting with the data. It copes with the version details X.509 protocols tend to have as well as with the many different versions and dialects.Applications must usually cope with all of this and it has to be coded over and over again. Libksba hides this by providing just one API which does the Right Thing™. Support for new features will be added as needed.
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
  --enable-shared \
	--enable-static

#CONFIGURE_ARGS += \
	--disable-rpath \
	--disable-asm \
	--disable-libksba-iconv \
	--disable-agent-support \
	--disable-bzip2 \
	--disable-ldap \
	--disable-finger \
	--disable-dns-srv \
	--disable-regex \

#MAKE_FLAGS += \
	SUBDIRS="m4 intl zlib util mpi cipher tools g10 keyserver ${checks}" \

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/bin $(2)/bin $(1)/usr/include $(1)/usr/lib $(1)/usr/share/aclocal
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/ksba-config $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/ksba*.h $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libksba.{la,a,so*} $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/aclocal/ksba.m4 $(1)/usr/share/aclocal/
	$(SED) 's,^libdir=\"$$$${exec_prefix}/lib,libdir=\"$(STAGING_DIR)/usr/lib,g' $(1)/usr/bin/ksba-config
	$(SED) 's,^includedir=\"$$$${prefix}/include/,includedir=\"$(STAGING_DIR)/usr/include/,g' $(1)/usr/bin/ksba-config
	ln -sf $(STAGING_DIR)/usr/bin/ksba-config $(2)/bin/
endef

define Package/libksba/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libksba.so.* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,libksba))
