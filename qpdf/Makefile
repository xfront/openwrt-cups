#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qpdf
PKG_VERSION:=10.6.3
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://download.fastgit.org/qpdf/qpdf/releases/download/release-$(PKG_NAME)-$(PKG_VERSION)/
PKG_MD5SUM:=440c70e3a5177087e5ac51b58371c043

TARGET_LDFLAGS+=-Wl,-rpath-link=$(STAGING_DIR)/usr/lib

PKG_MAINTAINER:=Val Kulkov <val.kulkov@gmail.com>
PKG_LICENSE:=FTL GPL-2.0-only MIT ZLIB GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE.txts
PKG_CPE_ID:=cpe:/a:qpdf:qpdf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libqpdf
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=A free, high-quality and portable font engine
  URL:=http://www.qpdf.org/
  DEPENDS:=+libstdcpp +zlib +libpng  +libjpeg +libatomic +libopenssl

endef

define Package/libqpdf/description
   Little CMS intends to be an OPEN SOURCE small-footprint color management engine,
   with special focus on accuracy and performance.
   It uses the International Color Consortium standard (ICC),
    which is the modern standard when regarding to color management.
endef

define Build/Configure
	$(call Build/Configure/Default, \
    --enable-crypto-openssl \
    --enable-insecure-random \
    --with-random=/dev/random \
	--disable-static \
		LIBS="$(TARGET_LDFLAGS)" \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libqpdf.* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libqpdf/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libqpdf.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libqpdf))

