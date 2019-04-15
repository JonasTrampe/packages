#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=python-markupsafe
PKG_VERSION:=1.1.1
PKG_RELEASE:=1

PKG_SOURCE:=MarkupSafe-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://files.pythonhosted.org/packages/b9/2e/64db92e53b86efccfaea71321f597fa2e1b2bd3853d8ce658568f7a13094/
PKG_HASH:=29872e92839765e546828bb7754a68c418d927cd064fd4708fab9fe9c8bb116b

PKG_BUILD_DIR:=$(BUILD_DIR)/python-markupsafe-$(PKG_VERSION)
PKG_UNPACK=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)
HOST_BUILD_DIR:=$(BUILD_DIR_HOST)/python-markupsafe-$(PKG_VERSION)
HOST_UNPACK=$(HOST_TAR) -C $(HOST_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)
PKG_USE_MIPS16:=0

HOST_BUILD_DEPENDS:=python python/host python-setuptools/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)
$(call include_mk, python-host.mk)

define Package/python-markupsafe
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  URL:=http://github.com/pallets/markupsafe/
  TITLE:=python-markupsafe
  DEPENDS:=+python +python-setuptools
endef

define Package/python-markupsafe/description
markupsafe is a microframework for Python based on Werkzeug, Jinja 2 and good
intentions. And before you ask: It.s BSD licensed!
endef

define Build/Compile
	$(call Build/Compile/PyMod,,\
		install --root="$(PKG_INSTALL_DIR)" --prefix="/usr" \
		--single-version-externally-managed \
	)
endef

define PyPackage/python-markupsafe/filespec
+|$(PYTHON_PKG_DIR)
-|$(PYTHON_PKG_DIR)/markupsafe/_vendor/distlib/*.exe
endef

define PyPackage/python-markupsafe/install
	$(INSTALL_DIR) $(1)/usr/lib $(1)/usr/bin
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

$(eval $(call PyPackage,python-markupsafe))
$(eval $(call BuildPackage,python-markupsafe))
