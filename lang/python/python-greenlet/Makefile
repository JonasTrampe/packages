# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-greenlet
PKG_VERSION:=0.4.15
PKG_RELEASE:=1

PKG_SOURCE:=greenlet-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://files.pythonhosted.org/packages/f8/e8/b30ae23b45f69aa3f024b46064c0ac8e5fcb4f22ace0dca8d6f9c8bbe5e7/
PKG_HASH:=9416443e219356e3c31f1f918a91badf2e37acf297e2fa13d24d1cc2380f8fbc
PKG_BUILD_DEPENDS:=python3
PKG_LICENSE:=Stackless Python
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Jonas Trampe <github@jonas-trampe.de>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_UNPACK=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)

include $(INCLUDE_DIR)/package.mk
include ../python3-package.mk

define Package/python3-greenlet
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=python3-greenlet
  DEPENDS:=+python3
endef

define Package/python3-greenlet/description
The greenlet package is a spin-off of Stackless, 
a version of CPython that supports micro-threads called "tasklets". 
Tasklets run pseudo-concurrently (typically in a single or a few OS-level threads) 
and are synchronized with data exchanges on "channels".

A "greenlet", on the other hand, is a still more primitive notion of micro-thread with no implicit scheduling; coroutines, 
in other words. This is useful when you want to control exactly when your code runs. 
You can build custom scheduled micro-threads on top of greenlet; however, 
it seems that greenlets are useful on their own as a way to make advanced control flow structures. 
For example, we can recreate generators; the difference with Python's own generators 
is that our generators can call nested functions and the nested functions can yield values too. 
Additionally, you don't need a "yield" keyword. See the example in tests/test_generator.py.

Greenlets are provided as a C extension module for the regular unmodified interpreter.

Greenlets are lightweight coroutines for in-process concurrent programming.
endef

define Py3Build/Compile
	$(call Build/Compile/Py3Mod,,\
		install --prefix="/usr" --root="$(PKG_INSTALL_DIR)" \
	)
endef

$(eval $(call Py3Package,python3-greenlet))
$(eval $(call BuildPackage,python3-greenlet))
