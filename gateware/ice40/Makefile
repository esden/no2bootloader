# Project config
PROJ = no2bootloader-ice40

PROJ_DEPS := no2usb no2misc no2ice40
PROJ_RTL_SRCS := $(addprefix rtl/, \
	dfu_helper.v \
	picorv32.v \
	picorv32_ice40_regs.v \
	soc_picorv32_bridge.v \
	soc_bram.v \
	soc_spram.v \
	sysmgr.v \
	wb_epbuf.v \
)
PROJ_SIM_SRCS := $(addprefix sim/, \
	spiflash.v \
)
PROJ_SIM_SRCS += rtl/top.v
PROJ_TESTBENCHES := \
	dfu_helper_tb \
	top_tb
PROJ_PREREQ = \
	$(BUILD_TMP)/boot.hex
PROJ_TOP_SRC := rtl/top.v
PROJ_TOP_MOD := top

# Target config
BOARD ?= icebreaker
DEVICE = up5k
PACKAGE = sg48

SEED ?= 10
NEXTPNR_ARGS = --pre-pack data/clocks.py --seed $(SEED)

# Include default rules
include ../build/project-rules.mk

# Custom rules
fw/boot.hex:
	make -C fw boot.hex

$(BUILD_TMP)/boot.hex: fw/boot.hex
	cp $< $@
