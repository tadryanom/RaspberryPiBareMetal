TARGET     = kernel8
TARGET_ELF = kernel8.elf
TARGET_IMG = kernel8.img

PREFIX  = aarch64-linux-gnu-
GCC     = $(PREFIX)gcc
LD      = $(PREFIX)ld
OBJCOPY = $(PREFIX)objcopy

SRCS = $(wildcard *.c)
OBJS = $(SRCS:.c=.o)
CFLAGS  = -Wall -O2 -ffreestanding -nostdinc -nostdlib -nostartfiles
LDFLAGS = -nostdlib -nostartfiles

%.o: %.S
	$(GCC) $(CFLAGS) -c $< -o $@

%.o: %.c
	$(GCC) $(CFLAGS) -c $< -o $@

$(TARGET_IMG): boot.o $(OBJS)
	$(LD) $(LDFLAGS) boot.o $(OBJS) -T linker.ld -o $(TARGET_ELF)
	$(OBJCOPY) -O binary $(TARGET_ELF) $(TARGET_IMG)

clean:
	rm $(TARGET_ELF) $(TARGET_IMG) *.o
