#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=python-click
PKG_VERSION:=7.0
PKG_RELEASE:=1

PKG_SOURCE:=Click-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://files.pythonhosted.org/packages/f8/5c/f60e9d8a1e77005f664b76ff8aeaee5bc05d0a91798afd7f53fc998dbc47/
PKG_HASH:=5b94b49521f6456670fdb30cd82a4eca9412788a93fa6dd6df72c94d5a8ff2d7

PKG_BUILD_DIR:=$(BUILD_DIR)/python-click-$(PKG_VERSION)
PKG_UNPACK=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)
HOST_BUILD_DIR:=$(BUILD_DIR_HOST)/python-click-$(PKG_VERSION)
HOST_UNPACK=$(HOST_TAR) -C $(HOST_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)
PKG_USE_MIPS16:=0

HOST_BUILD_DEPENDS:=python python/host python-setuptools/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)
$(call include_mk, python-host.mk)

define Package/python-click
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  URL:=http://github.com/pallets/click/
  TITLE:=python-click
  DEPENDS:=+python +python-setuptools
endef

define Package/python-click/description
click is a microframework for Python based on Werkzeug, Jinja 2 and good
intentions. And before you ask: It.s BSD licensed!
endef

define Build/Compile
	$(call Build/Compile/PyMod,,\
		install --root="$(PKG_INSTALL_DIR)" --prefix="/usr" \
		--single-version-externally-managed \
	)
endef

define PyPackage/python-click/filespec
+|$(PYTHON_PKG_DIR)
-|$(PYTHON_PKG_DIR)/click/_vendor/distlib/*.exe
endef

define PyPackage/python-click/install
	$(INSTALL_DIR) $(1)/usr/lib
	cp -r $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib
endef

define Host/Compile
	$(call Build/Compile/HostPyMod,,\
		install --root="$(STAGING_DIR_HOSTPKG)" --prefix="" \
		--single-version-externally-managed \
	)
endef

define Host/Install
endef

$(eval $(call HostBuild))

$(eval $(call PyPackage,python-click))
$(eval $(call BuildPackage,python-click))
