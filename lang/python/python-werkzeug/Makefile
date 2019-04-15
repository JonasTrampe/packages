#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=python-werkzeug
PKG_VERSION:=0.15.2
PKG_RELEASE:=1

PKG_SOURCE:=Werkzeug-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://files.pythonhosted.org/packages/f3/c8/fa7e1a0283267bee8efa10c665d8dca27e591face7e333c789c85671b3ab/
PKG_HASH:=0a73e8bb2ff2feecfc5d56e6f458f5b99290ef34f565ffb2665801ff7de6af7a

PKG_BUILD_DIR:=$(BUILD_DIR)/python-werkzeug-$(PKG_VERSION)
PKG_UNPACK=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)
HOST_BUILD_DIR:=$(BUILD_DIR_HOST)/python-werkzeug-$(PKG_VERSION)
HOST_UNPACK=$(HOST_TAR) -C $(HOST_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)
PKG_USE_MIPS16:=0

HOST_BUILD_DEPENDS:=python python/host python-setuptools/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)
$(call include_mk, python-host.mk)

define Package/python-werkzeug
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  URL:=http://github.com/pallets/werkzeug/
  TITLE:=python-werkzeug
  DEPENDS:=+python +python-setuptools
endef

define Package/python-werkzeug/description
werkzeug is a microframework for Python based on Werkzeug, Jinja 2 and good
intentions. And before you ask: It.s BSD licensed!
endef

define Build/Compile
	$(call Build/Compile/PyMod,,\
		install --root="$(PKG_INSTALL_DIR)" --prefix="/usr" \
		--single-version-externally-managed \
	)
endef

define PyPackage/python-werkzeug/filespec
+|$(PYTHON_PKG_DIR)
-|$(PYTHON_PKG_DIR)/werkzeug/_vendor/distlib/*.exe
endef

define PyPackage/python-werkzeug/install
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

$(eval $(call PyPackage,python-werkzeug))
$(eval $(call BuildPackage,python-werkzeug))
