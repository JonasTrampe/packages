#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=python-jinja2
PKG_VERSION:=2.10.1
PKG_RELEASE:=1

PKG_SOURCE:=Jinja2-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://files.pythonhosted.org/packages/93/ea/d884a06f8c7f9b7afbc8138b762e80479fb17aedbbe2b06515a12de9378d/
PKG_HASH:=065c4f02ebe7f7cf559e49ee5a95fb800a9e4528727aec6f24402a5374c65013

PKG_BUILD_DIR:=$(BUILD_DIR)/python-jinja2-$(PKG_VERSION)
PKG_UNPACK=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)
HOST_BUILD_DIR:=$(BUILD_DIR_HOST)/python-jinja2-$(PKG_VERSION)
HOST_UNPACK=$(HOST_TAR) -C $(HOST_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)
PKG_USE_MIPS16:=0

HOST_BUILD_DEPENDS:=python python/host python-setuptools/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)
$(call include_mk, python-host.mk)

define Package/python-jinja2
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  URL:=http://github.com/pallets/jinja2/
  TITLE:=python-jinja2
  DEPENDS:=+python +python-setuptools
endef

define Package/python-jinja2/description
jinja2 is a microframework for Python based on Werkzeug, Jinja 2 and good
intentions. And before you ask: It.s BSD licensed!
endef

define Build/Compile
	$(call Build/Compile/PyMod,,\
		install --root="$(PKG_INSTALL_DIR)" --prefix="/usr" \
		--single-version-externally-managed \
	)
endef

define PyPackage/python-jinja2/filespec
+|$(PYTHON_PKG_DIR)
-|$(PYTHON_PKG_DIR)/jinja2/_vendor/distlib/*.exe
endef

define PyPackage/python-jinja2/install
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

$(eval $(call PyPackage,python-jinja2))
$(eval $(call BuildPackage,python-jinja2))
