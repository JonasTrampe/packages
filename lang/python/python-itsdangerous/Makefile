#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=python-itsdangerous
PKG_VERSION:=1.1.0
PKG_RELEASE:=1

PKG_SOURCE:=itsdangerous-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://files.pythonhosted.org/packages/68/1a/f27de07a8a304ad5fa817bbe383d1238ac4396da447fa11ed937039fa04b/
PKG_HASH:=321b033d07f2a4136d3ec762eac9f16a10ccd60f53c0c91af90217ace7ba1f19

PKG_BUILD_DIR:=$(BUILD_DIR)/python-itsdangerous-$(PKG_VERSION)
PKG_UNPACK=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)
HOST_BUILD_DIR:=$(BUILD_DIR_HOST)/python-itsdangerous-$(PKG_VERSION)
HOST_UNPACK=$(HOST_TAR) -C $(HOST_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)
PKG_USE_MIPS16:=0

HOST_BUILD_DEPENDS:=python python/host python-setuptools/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)
$(call include_mk, python-host.mk)

define Package/python-itsdangerous
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  URL:=http://github.com/pallets/itsdangerous/
  TITLE:=python-itsdangerous
  DEPENDS:=+python +python-setuptools
endef

define Package/python-itsdangerous/description
itsdangerous is a microframework for Python based on Werkzeug, Jinja 2 and good
intentions. And before you ask: It.s BSD licensed!
endef

define Build/Compile
	$(call Build/Compile/PyMod,,\
		install --root="$(PKG_INSTALL_DIR)" --prefix="/usr" \
		--single-version-externally-managed \
	)
endef

define PyPackage/python-itsdangerous/filespec
+|$(PYTHON_PKG_DIR)
-|$(PYTHON_PKG_DIR)/itsdangerous/_vendor/distlib/*.exe
endef

define PyPackage/python-itsdangerous/install
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

$(eval $(call PyPackage,python-itsdangerous))
$(eval $(call BuildPackage,python-itsdangerous))
