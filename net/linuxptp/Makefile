#
# Copyright (C) 2015-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=linuxptp
PKG_VERSION:=3.1.1
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=@SF/$(PKG_NAME)/v$(PKG_VERSION)
PKG_HASH:=94d6855f9b7f2d8e9b0ca6d384e3fae6226ce6fc012dbad02608bdef3be1c0d9

PKG_MAINTAINER:=Wojciech Dubowik <Wojciech.Dubowik@westermo.com>
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYING
PKG_CPE_ID:=cpe:/a:linuxptp_project:linuxptp

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel.mk

define Package/linuxptp
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Time Synchronization
  TITLE:=Linux Precision Time Protocol (PTP) daemon
  URL:=http://linuxptp.sourceforge.net/
endef

define Package/linuxptp/description
 The PTP daemon (PTPd) implements version 2 of the Precision Time Protocol (PTP)
 as defined by the IEEE 1588-2008 standard.
 PTP was developed to provide very precise time coordination of LAN connected
 computers.
endef

EXTRA_CFLAGS += -DHAVE_CLOCK_ADJTIME -DHAVE_POSIX_SPAWN -DHAVE_ONESTEP_SYNC

MAKE_VARS += \
	EXTRA_CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS) $(EXTRA_CFLAGS)" \
	KBUILD_OUTPUT="$(LINUX_DIR)"

define Package/linuxptp/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hwstamp_ctl $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/phc2sys $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/phc_ctl $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pmc $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ptp4l $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/timemaster $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,linuxptp))
