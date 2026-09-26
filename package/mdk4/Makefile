include $(TOPDIR)/rules.mk

PKG_NAME:=mdk4
PKG_VERSION:=2024.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/aircrack-ng/mdk4.git
PKG_SOURCE_VERSION:=master

PKG_LICENSE:=GPL-2.0
PKG_MAINTAINER:=yourname <you@example.com>

include $(INCLUDE_DIR)/package.mk

define Package/mdk4
  SECTION:=net
  CATEGORY:=Network
  TITLE:=mdk4 - wireless testing tool (aircrack-ng)
  DEPENDS:=+libpcap
endef

define Package/mdk4/description
  mdk4 is a tool for testing and stress-testing wireless networks (successor to mdk3).
  Use only on networks you own or have explicit permission to test.
endef

define Build/Prepare
$(call Build/Prepare/Default)
endef

define Build/Compile
$(call Build/Compile/NoParallel)
if [ -f $(PKG_BUILD_DIR)/CMakeLists.txt ]; then \
mkdir -p $(PKG_BUILD_DIR)/build && cd $(PKG_BUILD_DIR)/build && \
cmake .. \
-DCMAKE_BUILD_TYPE=Release \
-DCMAKE_INSTALL_PREFIX=/usr \
-DCMAKE_C_COMPILER="$(TARGET_CC)" \
-DCMAKE_AR="$(TARGET_AR)" \
-DCMAKE_RANLIB="$(TARGET_RANLIB)" \
-DCMAKE_SYSROOT="$(STAGING_DIR)" \
-DCMAKE_C_FLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS) -I$(STAGING_DIR)/usr/include" \
-DCMAKE_EXE_LINKER_FLAGS="-L$(STAGING_DIR)/usr/lib" && \
$(MAKE) -j$(HOST_JOBS); \
else \
$(MAKE) -C $(PKG_BUILD_DIR) \
CC="$(TARGET_CC)" \
AR="$(TARGET_AR)" \
RANLIB="$(TARGET_RANLIB)" \
LD="$(TARGET_LD)" \
CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS) -I$(STAGING_DIR)/usr/include" \
LDFLAGS="$(TARGET_LDFLAGS) -L$(STAGING_DIR)/usr/lib" \
-j$(HOST_JOBS); \
fi
endef

define Package/mdk4/install
$(INSTALL_DIR) $(1)/usr/sbin
if [ -f $(PKG_BUILD_DIR)/mdk4 ]; then \
  $(INSTALL_BIN) $(PKG_BUILD_DIR)/mdk4 $(1)/usr/sbin/; \
elif [ -f $(PKG_BUILD_DIR)/build/mdk4 ]; then \
  $(INSTALL_BIN) $(PKG_BUILD_DIR)/build/mdk4 $(1)/usr/sbin/; \
elif [ -f $(PKG_BUILD_DIR)/src/mdk4 ]; then \
  $(INSTALL_BIN) $(PKG_BUILD_DIR)/src/mdk4 $(1)/usr/sbin/; \
else \
  echo "Error: mdk4 binary not found during install."; exit 1; \
fi
$(INSTALL_DIR) $(1)/usr/share/mdk4
endef

$(eval $(call BuildPackage,mdk4))
