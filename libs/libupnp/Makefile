#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# giveup@2017.2.7 update to git version

include $(TOPDIR)/rules.mk

PKG_NAME:=libupnp
PKG_VERSION:=1.8.0+git
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/mrjimenez/pupnp.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=eed7ec4aaab110beda25dbee539a1ed933b72c87
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.xz
PKG_MIRROR_MD5SUM:=228d09803efd95f1a55c856ac2ef1649
PKG_MAINTAINER:=Ted Hess <thess@kitschensync.net>

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libupnp/Default
  SECTION:=libs
  CATEGORY:=Libraries
  URL:=http://pupnp.sourceforge.net/
endef

define Package/libupnp
  $(call Package/libupnp/Default)
  DEPENDS:=+libpthread
  TITLE:=UPnP SDK library
  MENU:=1
endef

define Package/libupnp/description
The portable SDK for UPnP Devices (libupnp) provides developers with an API and
open source code for building control points, devices, and bridges that are
compliant with Version 1.0 of the  Universal Plug and Play Device Architecture
Specification.
endef

define Package/libupnp-sample
  $(call Package/libupnp/Default)
  DEPENDS:=libupnp
  TITLE:=UPnP sample applications
endef

define Package/libupnp-sample/description
TVcontrolpoint & tvdevice sample applications run inside /etc/upnp-tvdevice/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/upnp-1.8 $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/lib{ixml,threadutil,upnp}-1.8.{a,so*,la} $(1)/opt/lib/
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libupnp-1.8.pc $(1)/opt/lib/pkgconfig/
endef

define Package/libupnp/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/lib{ixml,threadutil,upnp}-1.8.so.* $(1)/opt/lib/
endef

define Package/libupnp-sample/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/upnp/sample/.libs/* $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/upnp-tvdevice/web
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/upnp/sample/web/* $(1)/etc/upnp-tvdevice
endef

$(eval $(call BuildPackage,libupnp))
$(eval $(call BuildPackage,libupnp-sample))
