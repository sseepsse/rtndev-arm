#
# Copyright (C) 2011-2015 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mp707
PKG_VERSION:=0.1.0
PKG_REV:=396233f9e4bb3dbb84f67f14fe32c1d9a2adf107
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=git://github.com/bubbafix/openwrt-bm1707.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/mp707
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+libusb-compat +libstdcpp
	TITLE:=USB thermometer MP707(BM1707) utility
	URL:=http://wl500g.info/showthread.php?20497&p=257339#post257339
	MAINTAINER:=Entware team, entware.wl500g.info
endef

define Package/mp707/description
 This utility works with USB thermometer MP707 (BM1707).
 More information on device can be found at http://www.masterkit.ru
endef

define Build/Compile
	$(TARGET_CXX) $(TARGET_CXXFLAGS) -c -I$(STAGING_DIR)/opt/include -o $(PKG_BUILD_DIR)/$(PKG_NAME).o $(PKG_BUILD_DIR)/package/bmtemp/src/bmtemp.cpp
	$(TARGET_CXX) $(TARGET_LDFLAGS) -L$(STAGING_DIR)/opt/lib -o $(PKG_BUILD_DIR)/bmtemp $(PKG_BUILD_DIR)/$(PKG_NAME).o -lusb
endef

define Package/mp707/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bmtemp $(1)/opt/bin
endef

$(eval $(call BuildPackage,mp707))
