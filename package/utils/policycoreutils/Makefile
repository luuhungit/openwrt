#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=policycoreutils
PKG_VERSION:=3.1
<<<<<<< HEAD
PKG_RELEASE:=2
=======
PKG_RELEASE:=5
>>>>>>> upstream/master

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/SELinuxProject/selinux/releases/download/20200710
PKG_HASH:=c889f62ee80f8b6a369469a9b8af51f5b797975aeaa291f5c5960cc12eed1934
PKG_INSTALL:=1
<<<<<<< HEAD
HOST_BUILD_DEPENDS:=libsemanage/host
PKG_BUILD_DEPENDS:=BUSYBOX_CONFIG_PAM:libpam
=======
HOST_BUILD_DEPENDS:=libsemanage/host gettext-full/host
PKG_BUILD_DEPENDS:=BUSYBOX_CONFIG_PAM:libpam gettext-full/host
>>>>>>> upstream/master

PKG_MAINTAINER:=Thomas Petazzoni <thomas.petazzoni@bootlin.com>
PKG_CPE_ID:=cpe:/a:selinuxproject:policycoreutils
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
<<<<<<< HEAD

define Package/policycoreutils
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:= +libsemanage +libcap-ng +BUSYBOX_CONFIG_PAM:libpam $(INTL_DEPENDS)
  TITLE:=SELinux policy utilities
  URL:=http://selinuxproject.org/page/Main_Page
  ALTERNATIVES:=\
    300:/sbin/restorecon:policycoreutils-restorecon \
    300:/sbin/setfiles:policycoreutils-setfiles \
    300:/usr/sbin/load_policy:policycoreutils-load_policy \
    300:/usr/sbin/sestatus:policycoreutils-sestatus \
    300:/usr/sbin/setsebool:policycoreutils-setsebool
endef

define Package/policycoreutils/description
	Policycoreutils is a collection of policy utilities
	(originally the "core" set of utilities needed to use
	SELinux, although it has grown a bit over time), which have
	different dependencies.  sestatus, secon, run_init, and
	newrole only use libselinux. load_policy and setfiles only
	use libselinux and libsepol. semodule and semanage use
	libsemanage (and thus bring in dependencies on libsepol and
	libselinux as well). setsebool uses libselinux to make
	non-persistent boolean changes (via the kernel interface)
	and uses libsemanage to make persistent boolean changes.
endef

include $(INCLUDE_DIR)/host-build.mk

HOST_MAKE_FLAGS += \
	PAMH=$(CONFIG_BUSYBOX_CONFIG_PAM) \
	PREFIX=$(STAGING_DIR_HOSTPKG) \
	SBINDIR=$(STAGING_DIR_HOSTPKG)/sbin \
	ETCDIR=$(STAGING_DIR_HOSTPKG)/etc

MAKE_FLAGS += \
	PAMH=$(CONFIG_BUSYBOX_CONFIG_PAM)

define Package/policycoreutils/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/sbin/restorecon_xattr $(1)/sbin/restorecon_xattr
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/sbin/restorecon $(1)/sbin/policycoreutils-restorecon
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/sbin/setfiles $(1)/sbin/policycoreutils-setfiles
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/fixfiles $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/genhomedircon $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/open_init_pty $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/run_init $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/semodule $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/load_policy $(1)/usr/sbin/policycoreutils-load_policy
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/sestatus $(1)/usr/sbin/policycoreutils-sestatus
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/setsebool $(1)/usr/sbin/policycoreutils-setsebool
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,policycoreutils))
=======
include $(INCLUDE_DIR)/host-build.mk

DIR_USR_BIN:= \
	newrole \
	secon

DIR_USR_SBIN:= \
	load_policy \
	sestatus \
	setsebool

LIBEXEC_UTILS := \
	pp

SBIN_UTILS:= \
	restorecon_xattr \
	setfiles

USR_BIN_UTILS:= \
	newrole \
	secon

USR_SBIN_UTILS:= \
	fixfiles \
	genhomedircon \
	open_init_pty \
	run_init \
	semodule \
	load_policy \
	sestatus \
	setsebool

TARGET_LDFLAGS += $(INTL_LDFLAGS) $(if $(INTL_FULL),-lintl)

MAKE_FLAGS += \
	PAMH=$(CONFIG_BUSYBOX_CONFIG_PAM)

HOST_MAKE_FLAGS += \
	PAMH=$(CONFIG_BUSYBOX_CONFIG_PAM) \
	DESTDIR=$(STAGING_DIR_HOST) \
	PREFIX= \
	SBINDIR=/bin

HOST_LDFLAGS += -Wl,-rpath=$(STAGING_DIR_HOSTPKG)/lib

$(eval $(foreach a,$(DIR_SBIN),ALTS_$(a):=300:/sbin/$(a):/sbin/policycoreutils-$(a)$(newline)))
$(eval $(foreach a,$(DIR_USR_BIN),ALTS_$(a):=300:/usr/bin/$(a):/usr/bin/policycoreutils-$(a)$(newline)))
$(eval $(foreach a,$(DIR_USR_SBIN),ALTS_$(a):=300:/usr/sbin/$(a):/usr/sbin/policycoreutils-$(a)$(newline)))
ALTS_setfiles:=300:/sbin/restorecon:/sbin/policycoreutils-setfiles 300:/sbin/setfiles:/sbin/policycoreutils-setfiles

DEPENDS_genhomedircon:=+libsemanage $(INTL_DEPENDS)
DEPENDS_load_policy:=+libselinux $(INTL_DEPENDS)
DEPENDS_newrole:=+libselinux +libaudit +BUSYBOX_CONFIG_PAM:libpam $(INTL_DEPENDS)
DEPENDS_open_init_pty:=$(INTL_DEPENDS)
DEPENDS_pp:=+libsepol $(INTL_DEPENDS)
DEPENDS_restorecon_xattr:=+libselinux +libsepol +libaudit $(INTL_DEPENDS)
DEPENDS_run_init:=+libselinux +libaudit +BUSYBOX_CONFIG_PAM:libpam $(INTL_DEPENDS)
DEPENDS_secon:=+libselinux $(INTL_DEPENDS)
DEPENDS_semanage:=+libsemanage
DEPENDS_semodule:=+libsemanage $(INTL_DEPENDS)
DEPENDS_sestatus:=+libselinux $(INTL_DEPENDS)
DEPENDS_setfiles:=+libselinux +libsepol +libaudit $(INTL_DEPENDS)
DEPENDS_setsebool:=+libsemanage $(INTL_DEPENDS)

define Package/policycoreutils/Default
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=SELinux policy utility
  URL:=http://selinuxproject.org/page/Main_Page
endef

define Package/policycoreutils
  $(call Package/policycoreutils/Default)
  MENU:=1
  TITLE+= common files
endef

define GenUtilPkg
  define Package/$(1)
    $(call Package/policycoreutils/Default)
    DEPENDS+= policycoreutils $(DEPENDS_$(2))
    TITLE+= $(2)
    ALTERNATIVES:=$(ALTS_$(2))
  endef

  define Package/$(1)/description
Policycoreutils is a collection of policy utilities
(originally the "core" set of utilities needed to use
SELinux, although it has grown a bit over time).

This package provides the $(2) utility.
  endef
endef

$(foreach a,$(LIBEXEC_UTILS) $(SBIN_UTILS) $(USR_BIN_UTILS) $(USR_SBIN_UTILS),$(eval $(call GenUtilPkg,policycoreutils-$(a),$(a))))

define Package/policycoreutils/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/sestatus.conf $(1)/etc
ifdef CONFIG_BUSYBOX_CONFIG_PAM
	$(INSTALL_DIR) $(1)/etc/pam.d
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/pam.d/run_init $(1)/etc/pam.d
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/pam.d/newrole $(1)/etc/pam.d
endif
endef

define BuildUtil
  define Package/$(1)/install
	$(INSTALL_DIR) $$(1)$(2)
	$(INSTALL_BIN) $$(PKG_INSTALL_DIR)$(2)/$(3) $$(1)$(2)/$(if $(ALTS_$(3)),policycoreutils-$(3),$(3))
  endef

  $$(eval $$(call BuildPackage,$(1)))
endef

$(eval $(call BuildPackage,policycoreutils))
$(foreach a,$(SBIN_UTILS),$(eval $(call BuildUtil,policycoreutils-$(a),/sbin,$(a))))
$(foreach a,$(USR_BIN_UTILS),$(eval $(call BuildUtil,policycoreutils-$(a),/usr/bin,$(a))))
$(foreach a,$(USR_SBIN_UTILS),$(eval $(call BuildUtil,policycoreutils-$(a),/usr/sbin,$(a))))
$(foreach a,$(LIBEXEC_UTILS),$(eval $(call BuildUtil,policycoreutils-$(a),/usr/libexec/selinux/hll,$(a))))
$(eval $(call HostBuild))
>>>>>>> upstream/master
