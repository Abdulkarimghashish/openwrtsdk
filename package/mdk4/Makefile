include $(TOPDIR)/rules.mk

PKG_NAME:=mdk4
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/aircrack-ng/mdk4.git
PKG_SOURCE_DATE:=2023-01-26
PKG_SOURCE_VERSION:=v4.2
PKG_HASH:=skip

PKG_MAINTAINER:=OpenWrt Community
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/mdk4
  SECTION:=net
  CATEGORY:=Network
  TITLE:=MDK4 is a proof-of-concept tool to exploit 802.11 networks
  URL:=https://github.com/aircrack-ng/mdk4
  DEPENDS:=+libnl-tiny +libpcap
endef

define Package/mdk4/description
  MDK4 is a professional wireless attack tool for Linux and OS X,
  designed to evaluate the security of 802.11 networks.
endef

define Build/Compile
$(MAKE) -C $(PKG_BUILD_DIR) \
CC="$(TARGET_CC)" \
CFLAGS="$(TARGET_CFLAGS)" \
LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/mdk4/install
$(INSTALL_DIR) $(1)/usr/bin
$(INSTALL_BIN) $(PKG_BUILD_DIR)/mdk4 $(1)/usr/bin/
endef

$(eval $(call BuildPackage,mdk4))
