#
# Copyright (C) 2009-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=prosody-devel
PKG_REV:=6f97acc4583b
PKG_VERSION:=r$(PKG_REV)
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=hg
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://hg.prosody.im/0.11/
#PKG_HASH:=1a59a322b71928a21985522aa00d0eab3552208d7bf9ecb318542a1b2fee3e8d
PKG_MAINTAINER:=Thomas Heil <heil@terminal-consulting.de>
PKG_LICENSE:=MIT/X11

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/prosody-devel
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Instant Messaging
  DEPENDS:=+luafilesystem +libidn +luaexpat +luasec +libopenssl +libidn +liblua 
  TITLE:=XMPP server
  URL:=http://prosody.im/
  USERID:=prosody=54:prosody=54
endef

define Package/prosody-devel/description
  Prosody is an exciting new server for Jabber/XMPP
  written in Lua. It aims to be easy to use, and light
  on resources
endef

define Package/prosody-devel/conffiles
/etc/prosody/prosody.cfg.lua
endef

TARGET_CFLAGS += $(FPIC) -DWITHOUT_MALLINFO 

TARGET_LDFLAGS += -L$(STAGING_DIR)/usr/lib 


define Build/Configure
	# this is *NOT* GNU autoconf stuff
	(cd $(PKG_BUILD_DIR); ./configure \
		--prefix=/usr \
		--with-lua="$(STAGING_DIR_HOSTPKG)" \
		--with-lua-include="$(STAGING_DIR)/usr/include" \
		--with-lua-lib="$(STAGING_DIR)/usr/lib" \
		--cflags="$(TARGET_CFLAGS)" \
		--ldflags="$(TARGET_LDFLAGS) -llua -lm -ldl -shared" \
		--c-compiler="$(CC)" \
		--linker="$(LD)" \
		--datadir="/etc/prosody/data" \
	)
endef
#	LDFLAGS="$(TARGET_LDFLAGS) -llua -lm -ldl" \

MAKE_FLAGS += \
	CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS) -std=gnu99" \
	PREFIX="/usr" \

define Package/prosody-devel/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/prosody.init $(1)/etc/init.d/prosody
	$(INSTALL_DIR) $(1)/etc/prosody
	#$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/prosody/prosody.cfg.lua $(1)/etc/prosody/
	$(INSTALL_CONF) ./files/prosody.cfg.lua $(1)/etc/prosody/
	$(INSTALL_DIR) $(1)/etc/prosody/certs
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/etc/prosody/certs/localhost.{crt,key} $(1)/etc/prosody/certs/
	$(INSTALL_DIR) $(1)/etc/prosody/data
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/prosody{,ctl} $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/lib/prosody
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/prosody/prosody.version $(1)/usr/lib/prosody/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/core
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/core/*.lua $(1)/usr/lib/prosody/core/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/fallbacks
	#$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/fallbacks/*.lua $(1)/usr/lib/prosody/fallbacks/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/modules
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/modules/*.lua $(1)/usr/lib/prosody/modules/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/modules/adhoc
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/modules/adhoc/*.lua $(1)/usr/lib/prosody/modules/adhoc/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/modules/mod_mam
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/modules/mod_mam/*.lua $(1)/usr/lib/prosody/modules/mod_mam/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/modules/mod_pubsub
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/modules/mod_pubsub/*.lua $(1)/usr/lib/prosody/modules/mod_pubsub/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/modules/mod_s2s
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/modules/mod_s2s/*.lua $(1)/usr/lib/prosody/modules/mod_s2s/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/modules/muc
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/modules/muc/*.lua $(1)/usr/lib/prosody/modules/muc/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/net
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/net/*.lua $(1)/usr/lib/prosody/net/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/net/http
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/net/http/*.lua $(1)/usr/lib/prosody/net/http/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/net/resolvers
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/net/resolvers/*.lua $(1)/usr/lib/prosody/net/resolvers/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/net/websocket
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/net/websocket/*.lua $(1)/usr/lib/prosody/net/websocket/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/util
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/util/*.lua $(1)/usr/lib/prosody/util/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/prosody/util/*.so $(1)/usr/lib/prosody/util/
	$(INSTALL_DIR) $(1)/usr/lib/prosody/util/sasl
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/prosody/util/sasl/*.lua $(1)/usr/lib/prosody/util/sasl/
	#$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/prosody/util/sasl/*.so $(1)/usr/lib/prosody/util/sasl/
endef

define Package/prosody-devel/postinst
#!/bin/sh
[ -n "$${IPKG_INSTROOT}" ] || {
	echo "Fixing lua with paxctl if needed!!!"
	[ -f /sbin/paxctl ] && {
		paxctl  -v /usr/bin/ > /dev/null  2>&1
		[ $$? -ne 0 ] && {
			cp /usr/bin/lua /tmp
			paxctl -c -m /tmp/lua > /dev/null  2>&1 
			cp -f /tmp/lua /usr/bin/lua
		}
	}
	exit 0
}
endef

$(eval $(call BuildPackage,prosody-devel))
