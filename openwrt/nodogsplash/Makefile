#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nodogsplash
PKG_FIXUP:=autoreconf
PKG_VERSION:=4.0.3beta
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://codeload.github.com/nodogsplash/nodogsplash/tar.gz/v$(PKG_VERSION)?
PKG_SOURCE:=nodogsplash-$(PKG_VERSION).tar.gz
PKG_HASH:= #shasum -a 256 of tar.gz of source files goes here
PKG_BUILD_DIR:=$(BUILD_DIR)/nodogsplash-$(PKG_VERSION)

PKG_MAINTAINER:=Moritz Warning <moritzwarning@web.de>
PKG_BUILD_PARALLEL:=1
PKG_LICENSE:=GPL-2.0+

include $(INCLUDE_DIR)/package.mk


define Package/nodogsplash
	SUBMENU:=Captive Portals
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+libpthread +iptables-mod-ipopt +libmicrohttpd-no-ssl
	TITLE:=Open public network gateway daemon
	URL:=https://github.com/nodogsplash/nodogsplash
	CONFLICTS:=nodogsplash2
endef

define Package/nodogsplash/description
	Nodogsplash is a Captive Portal that offers a simple way to
	provide restricted access to the Internet by showing a splash
	page to the user before Internet access is granted.
	It also incorporates an API that allows the creation of
	sophisticated authentication applications.
endef

define Package/nodogsplash/install

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/nodogsplash $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ndsctl $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/nodogsplash/htdocs/images
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_DIR) $(1)/usr/lib/nodogsplash
	$(CP) $(PKG_BUILD_DIR)/resources/splash.html $(1)/etc/nodogsplash/htdocs/
	$(CP) $(PKG_BUILD_DIR)/resources/splash.css $(1)/etc/nodogsplash/htdocs/
	$(CP) $(PKG_BUILD_DIR)/resources/status.html $(1)/etc/nodogsplash/htdocs/
	$(CP) $(PKG_BUILD_DIR)/resources/splash.jpg $(1)/etc/nodogsplash/htdocs/images/
	$(CP) $(PKG_BUILD_DIR)/openwrt/nodogsplash/files/etc/config/nodogsplash $(1)/etc/config/
	$(CP) $(PKG_BUILD_DIR)/openwrt/nodogsplash/files/etc/init.d/nodogsplash $(1)/etc/init.d/
	$(CP) $(PKG_BUILD_DIR)/openwrt/nodogsplash/files/etc/uci-defaults/40_nodogsplash $(1)/etc/uci-defaults/
	$(CP) $(PKG_BUILD_DIR)/openwrt/nodogsplash/files/usr/lib/nodogsplash/restart.sh $(1)/usr/lib/nodogsplash/
	$(CP) $(PKG_BUILD_DIR)/forward_authentication_service/PreAuth/demo-preauth.sh $(1)/usr/lib/nodogsplash/login.sh
	$(CP) $(PKG_BUILD_DIR)/forward_authentication_service/fas-aes/fas-aes.php $(1)/etc/nodogsplash/
endef

define Package/nodogsplash/postrm
#!/bin/sh
uci delete firewall.nodogsplash
uci commit firewall
endef

define Package/nodogsplash/conffiles
/etc/config/nodogsplash
endef

$(eval $(call BuildPackage,nodogsplash))
