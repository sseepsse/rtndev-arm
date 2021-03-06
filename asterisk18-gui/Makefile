#
# Copyright (C) 2014 OpenWrt.org, abandoned
# Copyright (C) 2015 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=asterisk18-gui
PKG_VERSION:=2.1.0-rc1
PKG_RELEASE:=1

PKG_SOURCE_URL:=http://downloads.asterisk.org/pub/telephony/asterisk-gui/releases/
PKG_SOURCE:=asterisk-gui-$(PKG_VERSION).tar.gz
PKG_MD5SUM:=055bf2aaba365e696198925d039ac3cb
PKG_BUILD_DIR:=$(BUILD_DIR)/asterisk18-gui-$(PKG_VERSION)

PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYING LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/asterisk18-gui
  SECTION:=admin
  CATEGORY:=Administration
  TITLE:=Asterisk GUI for Asterisk 1.8.x
  DEPENDS:=+@PACKAGE_asterisk18 +asterisk18-chan-local +asterisk18-app-exec +asterisk18-app-system
  VERSION:=$(PKG_VERSION)
endef

define Package/asterisk18-gui/description
 Asterisk18 GUI is a framework for the creation of graphical interfaces 
 for configuring Asterisk-1.8.x package.
endef

EXTRA_CFLAGS:=$(TARGET_CPPFLAGS)
EXTRA_LDFLAGS:=$(TARGET_LDFLAGS)

define Build/Prepare
	rm -rf $(PKG_BUILD_DIR)/
	mkdir -p $(PKG_BUILD_DIR)/
	$(TAR) -xzf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR) --strip 1
	$(Build/Patch)
endef

define Build/Configure
	( cd $(PKG_BUILD_DIR); ./bootstrap.sh )
	$(call Build/Configure/Default, \
			--build=$(GNU_HOST_NAME) \
			--host=$(GNU_TARGET_NAME) \
			--target=$(GNU_TARGET_NAME) \
			--prefix=/opt \
			--disable-nls \
			--disable-static \
			--localstatedir="/opt" \
			--sysconfdir="/opt/etc" \
		)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR="$(PKG_INSTALL_DIR)"
	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR="$(PKG_INSTALL_DIR)" install
endef

define Package/asterisk18-gui/install
	$(INSTALL_DIR) $(1)/opt/etc/asterisk/
	$(CP) ./files/gui_* $(1)/opt/etc/asterisk/
	$(INSTALL_DIR) $(1)/opt/lib/asterisk/static-http
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/asterisk/static-http/* $(1)/opt/lib/asterisk/static-http
	$(INSTALL_DIR) $(1)/opt/lib/asterisk/scripts
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/asterisk/scripts/* $(1)/opt/lib/asterisk/scripts
	$(INSTALL_DIR) $(1)/opt/lib/asterisk/gui_backups
endef

$(eval $(call BuildPackage,asterisk18-gui))
