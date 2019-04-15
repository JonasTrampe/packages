#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=python-flask
PKG_VERSION:=1.0.3
PKG_RELEASE:=1

PKG_SOURCE:=Flask-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/JonasTrampe/flask/releases/download/$(PKG_VERSION)/
PKG_HASH:=90087c0010a289caa22fd60c57eb4fd5f5ea09b5adb950c599b0e9cde94ef625

PKG_BUILD_DIR:=$(BUILD_DIR)/python-flask-$(PKG_VERSION)
PKG_UNPACK=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)
HOST_BUILD_DIR:=$(BUILD_DIR_HOST)/python-flask-$(PKG_VERSION)
HOST_UNPACK=$(HOST_TAR) -C $(HOST_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)
PKG_USE_MIPS16:=0

HOST_BUILD_DEPENDS:=python python/host python-setuptools/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)
$(call include_mk, python-host.mk)

define Package/python-flask
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  URL:=http://github.com/pallets/flask/
  TITLE:=python-flask
  DEPENDS:=+python-click +python-codecs +python-decimal \
           +python-itsdangerous +python-jinja2 +python +python-logging \
           +python-markupsafe +python-multiprocessing +python-setuptools \
           +python-werkzeug
endef

define Package/python-flask/description
Flask is a microframework for Python based on Werkzeug, Jinja 2 and good
intentions. And before you ask: It.s BSD licensed!
endef

define Build/Compile
	$(call Build/Compile/PyMod,,\
		install --root="$(PKG_INSTALL_DIR)" --prefix="/usr" \
		--single-version-externally-managed \
	)
endef

define PyPackage/python-flask/filespec
+|$(PYTHON_PKG_DIR)
-|$(PYTHON_PKG_DIR)/flask/_vendor/distlib/*.exe
endef

define PyPackage/python-flask/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/etc
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin
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

$(eval $(call PyPackage,python-flask))
$(eval $(call BuildPackage,python-flask))
