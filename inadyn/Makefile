#
# Copyright (C) 2011-2015 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=inadyn
PKG_VERSION:=1.99.14-20150210
PKG_RELEASE:=1

PKG_REV:=7256141c6bd6d1ed0d427197fc08cc98731918f0
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/troglobit/inadyn
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/inadyn
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=IP Addresses and Names
	DEPENDS:=+libgnutls-openssl
	TITLE:=a simple and small DDNS client
	URL:=https://github.com/vampik/inadyn
	MAINTAINER:=Entware team, entware.wl500g.info
endef

define Package/inadyn/description
 Inadyn is a simple and small DDNS client written in the C language. It can
 maintain multiple host names with the same IP address, and has a web based
 IP detection which runs well behind a NAT router. This is a fork by
 Andrey Tikhomirov.
endef

TARGET_CFLAGS += -Iinclude

define Package/inadyn/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/inadyn $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_CONF) ./files/inadyn.conf $(1)/opt/etc/
	$(INSTALL_BIN) ./files/S52inadyn $(1)/opt/etc/init.d/
endef

define Package/inadyn/conffiles
/opt/etc/inadyn.conf
endef

$(eval $(call BuildPackage,inadyn))
