# SPDX-License-Identifier: GPL-2.0-only

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

KERNEL_LOADADDR = 0x80000000
KERNEL_ENTRY = 0x80000400

define Device/Default
  PROFILES = Default
  KERNEL := kernel-bin | append-dtb | gzip | uImage gzip
  KERNEL_INITRAMFS := kernel-bin | append-dtb | gzip | uImage gzip
  DEVICE_DTS_DIR := ../dts
  DEVICE_DTS = $$(SOC)_$(1)
  SUPPORTED_DEVICES := $(subst _,$(comma),$(1))
  IMAGES := sysupgrade.bin
  IMAGE/sysupgrade.bin := append-kernel | pad-to 64k | append-rootfs | pad-rootfs | \
	append-metadata | check-size
endef

# "NGE" refers to the uImage magic
define Device/netgear_nge
  KERNEL := kernel-bin | append-dtb | lzma | uImage lzma
  KERNEL_INITRAMFS := kernel-bin | append-dtb | lzma | uImage lzma
  SOC := rtl8380
  IMAGE_SIZE := 14848k
  UIMAGE_MAGIC := 0x4e474520
  DEVICE_VENDOR := NETGEAR
endef

define Device/allnet_all-sg8208m
  SOC := rtl8382
  IMAGE_SIZE := 7168k
  DEVICE_VENDOR := ALLNET
  DEVICE_MODEL := ALL-SG8208M
  UIMAGE_MAGIC := 0x00000006
  UIMAGE_NAME := 2.2.2.0
endef
TARGET_DEVICES += allnet_all-sg8208m

define Device/d-link_dgs-1210
  SOC := rtl8382
  IMAGE_SIZE := 13824k
  DEVICE_VENDOR := D-Link
endef

define Device/d-link_dgs-1210-10p
  $(Device/d-link_dgs-1210)
  DEVICE_MODEL := DGS-1210-10P
  DEVICE_PACKAGES += lua-rs232
endef
TARGET_DEVICES += d-link_dgs-1210-10p

define Device/d-link_dgs-1210-16
  $(Device/d-link_dgs-1210)
  DEVICE_MODEL := DGS-1210-16
endef
TARGET_DEVICES += d-link_dgs-1210-16

define Device/d-link_dgs-1210-28
  $(Device/d-link_dgs-1210)
  DEVICE_MODEL := DGS-1210-28
endef
TARGET_DEVICES += d-link_dgs-1210-28

define Device/netgear_gs108t-v3
  $(Device/netgear_nge)
  DEVICE_MODEL := GS108T
  DEVICE_VARIANT := v3
endef
TARGET_DEVICES += netgear_gs108t-v3

define Device/netgear_gs110tpp-v1
  $(Device/netgear_nge)
  DEVICE_MODEL := GS110TPP
  DEVICE_VARIANT := v1
endef
TARGET_DEVICES += netgear_gs110tpp-v1

define Device/zyxel_gs1900-10hp
  SOC := rtl8380
  IMAGE_SIZE := 6976k
  DEVICE_VENDOR := Zyxel
  DEVICE_MODEL := GS1900-10HP
endef
TARGET_DEVICES += zyxel_gs1900-10hp

$(eval $(call BuildImage))
