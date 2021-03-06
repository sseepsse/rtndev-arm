#
# Copyright (C) 2011-2015 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#


include $(TOPDIR)/rules.mk

PKG_NAME:=python-chardet
PKG_VERSION:=2.3.0
PKG_RELEASE:=1

PKG_SOURCE:=chardet-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://pypi.python.org/packages/source/c/chardet/
PKG_MD5SUM:=25274d664ccb5130adae08047416e1a8
PKG_BUILD_DIR:=$(BUILD_DIR)/chardet-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

PKG_BUILD_DEPENDS:=python distribute/host

define Package/$(PKG_NAME)
	SUBMENU:=Python
	SECTION:=lang
	CATEGORY:=Languages
	TITLE:=Python universal enconding detector
	URL:=https://github.com/erikrose/chardet
	DEPENDS:=+python
	MAINTAINER:=Entware team, entware.wl500g.info
endef

define Package/$(PKG_NAME)/description
 Chardet guesses the encoding of text files. Includes a command-line script
 which reports on the encodings of one or more files.
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix=/opt --root=$(PKG_INSTALL_DIR))
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
	    $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
	    $(1)$(PYTHON_PKG_DIR)/
	$(INSTALL_DIR) $(1)/opt/bin
	 $(SED) 's,$(STAGING_DIR)/opt/bin/hostpython,/opt/bin/python,g' $(PKG_INSTALL_DIR)/opt/bin/chardetect
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/chardetect $(1)/opt/bin/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
