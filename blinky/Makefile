# Author: Yusef Karim

##### Project setup #####
# Name of your current project
PROJ_NAME = $(shell basename $(CURDIR))
# Directory containing all CMSIS relevent source code
CMSIS_DIR ?= ${TOOLS_PATH}
LINKER_SCRIPT ?= $(CMSIS_DIR)/STM32L476RG.ld

##### Toolchain #####
TRIPLE  = 	arm-none-eabi
CC 		=	${TRIPLE}-gcc
LD 		= 	${TRIPLE}-ld
AS 		= 	${TRIPLE}-as
GDB 	= 	${TRIPLE}-gdb
OBJCOPY =  	${TRIPLE}-objcopy

##### Compiler options #####
CFLAGS = -g -Wall $(if $(LINKER_SCRIPT),-T$(LINKER_SCRIPT),)
CFLAGS += -mlittle-endian -mthumb -mcpu=cortex-m4
CFLAGS += -mfloat-abi=hard -mfpu=fpv4-sp-d16 --specs=nosys.specs

##### Project specific libraries #####
SRC_FILES += $(wildcard src/*.c)
CFLAGS += -Iinc

##### CMSIS libraries and source code (optional) #####
ifneq ($(strip $(CMSIS_DIR)),)
	ifneq ($(wildcard $(CMSIS_DIR)),)
		SRC_FILES += $(CMSIS_DIR)/src/*
		CFLAGS += -I$(CMSIS_DIR)/inc
	endif
endif

all:  $(PROJ_NAME).bin

##### Flash code to board using OpenOCD #####
flash: $(PROJ_NAME).bin
	st-flash write $^ 0x08000000 


clean:
	rm -f $(PROJ_NAME).bin $(PROJ_NAME).elf

$(PROJ_NAME).elf: $(SRC_FILES)
	$(CC) $(CFLAGS) -o $@ $^

$(PROJ_NAME).bin: $(PROJ_NAME).elf
	$(OBJCOPY) -O binary $^ $@

