# 
# Copyright (C) 2006-2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lxc
PKG_RELEASE:=1
PKG_SOURCE_URL:=@SF/lxc

PKG_VERSION:=0.7.5
PKG_MD5SUM:=cf001ad3f465b17d48dfd623b0011e73
#PKG_VERSION:=0.7.4.2
#PKG_MD5SUM:=36fcb0f6a39d2f55130421f342f24ef3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel.mk

define Package/lxc
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=LXC userspace tools
  URL:=http://lxc.sourceforge.net/

  DEPENDS:= +libcap2 +bash +@BUSYBOX_CONFIG_GETOPT \
            +ip +patch +diffutils +coreutils +coreutils-rm \
            +perlbase-complete +perlbase-base +perlbase-getcwd +perlbase-getopt +perlbase-sys 

  MDEPENDS:=@USE_EGLIBC
endef

define Package/lxc/description
	Userspace tools to manage linux containers
endef

define Build/Configure
$(call Build/Configure/Default,--with-linuxdir=$(LINUX_DIR))
endef

define Package/lxc/install

	$(INSTALL_DIR) $(1)/lxc
	$(INSTALL_DIR) $(1)/cgroup
	$(INSTALL_DIR) $(1)/tmp/lib
	ln -s /lxc $(1)/tmp/lib/lxc
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/lxc.init $(1)/etc/init.d/lxc

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_BIN) ./files/lxc.config_lxc $(1)/etc/config/lxc
#	$(INSTALL_BIN) ./files/lxc.config_network $(1)/etc/config/network

	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) ./files/lxc.checkconfig $(1)/sbin/
	$(INSTALL_BIN) ./files/lxc.configure $(1)/sbin/
	$(INSTALL_BIN) ./files/lxc.openwrt $(1)/sbin/
	$(INSTALL_BIN) ./files/lxc.debian $(1)/sbin/



	$(INSTALL_DIR) $(1)/usr/bin	
	$(INSTALL_DIR) $(1)/usr/lib
#	$(INSTALL_DIR) $(1)/tmp/lib
#	$(INSTALL_DIR) $(1)/tmp/lib/lxc/
	$(INSTALL_DIR) $(1)/usr/lib/lxc/rootfs
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-attach $(1)/usr/bin/lxc-attach
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-unshare $(1)/usr/bin/lxc-unshare
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-stop $(1)/usr/bin/lxc-stop
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-start $(1)/usr/bin/lxc-start
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-wait $(1)/usr/bin/lxc-wait
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-console $(1)/usr/bin/lxc-console
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-freeze $(1)/usr/bin/lxc-freeze
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-info $(1)/usr/bin/lxc-info
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-cgroup $(1)/usr/bin/lxc-cgroup
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-unfreeze $(1)/usr/bin/lxc-unfreeze
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-checkpoint $(1)/usr/bin/lxc-checkpoint
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-restart $(1)/usr/bin/lxc-restart
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-kill $(1)/usr/bin/lxc-kill
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-create $(1)/usr/bin/lxc-create
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-destroy $(1)/usr/bin/lxc-destroy
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-netstat $(1)/usr/bin/lxc-netstat
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-ps $(1)/usr/bin/lxc-ps
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-ls $(1)/usr/bin/lxc-ls
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-setcap $(1)/usr/bin/lxc-setcap
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-version $(1)/usr/bin/lxc-version
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-checkconfig $(1)/usr/bin/lxc-checkconfig
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lxc/lxc-monitor $(1)/usr/bin/lxc-monitor
	$(CP)  $(PKG_BUILD_DIR)/src/lxc/liblxc* $(1)/usr/lib/
	ln -s liblxc.so $(1)/usr/lib/liblxc.so.0
endef

$(eval $(call BuildPackage,lxc))
