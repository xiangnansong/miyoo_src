# A basic Makefile to compile for Gp2x. SDL version

CC = arm-linux-gcc
LD = arm-linux-gcc
STRIP = arm-linux-strip

NAME=lemonboy2x
TARGET=../$(NAME)-sdl.gpe

DEFS = -DLEMONBOY -DGP2X -DGLOBAL_CONFIG_FILE=etc/system.gp2x -DIS_LITTLE_ENDIAN -D_REENTRANT -DSUPERGB -DGP2X_ASM

#CFLAGS = -mcpu=arm926ej-s -fsigned-char \
#-O3 -msoft-float -ffast-math -fomit-frame-pointer -fstrict-aliasing \
#-mstructure-size-boundary=32 -fexpensive-optimizations \
#-fweb -frename-registers -falign-functions=16 -falign-loops -falign-labels -falign-jumps \
#-finline -finline-functions -fno-common -fno-builtin \
#-Wunused
#-Wall -Wno-sign-compare -Wunused -Wpointer-arith -Wcast-align -Waggregate-return -Wshadow

INCS =  -I. -I/opt/miyoo/arm-miyoo-linux-uclibcgnueabi/sysroot/usr/include/SDL

LDFLAGS=$(CFLAGS)
LIBS = -lSDL -lpng -lm -lz -lpthread

#DEBUG=-DDEBUG

include Version

SDL_OBJS = sys/sdl/sdl.o sys/sdl/keymap.o  sys/sdl/memcpy.o sys/sdl/memset.o
OBJS = lcd.o refresh.o lcdc.o palette.o cpu.o mem.o rtc.o hw.o sound.o \
	events.o keytable.o \
	loader.o save.o emu.o main.o \
	rccmds.o rckeys.o rcvars.o rcfile.o exports.o \
	unzip/unzip.o unzip/ioapi.o split.o path.o inflate.o supergb.o \
	gui/menu.o gui/utils.o gui/imaging.o gui/options.o sys/nix/nix.o $(SDL_OBJS)


MYCC = $(CC) $(CFLAGS) $(INCS) $(DEBUG) $(PROFILING) $(DEFS)
MYAS = $(CC) $(ASFLAGS)

VERSION = `cat $(PWD)/Version | awk '/VERSION =/ {printf("%s", $$3); }'`

########################################################################

sdl: $(TARGET)


$(TARGET): $(OBJS) $(SDL_OBJS)
	$(LD) $(LDFLAGS) $(PROFILING) $(OBJS) -o $@ $(LIBS)
	$(STRIP) $@

main.o: Version

.c.o:
	$(MYCC) -c $< -o $@

.S.o:
	$(MYAS) -c $< -o $@

clean:
	rm -f *.o sys/*.o sys/*/*.o unzip/*.o gio/*.o *~ sys/*/*~ sys/*~ gui/*~ unzip/*~ gui/*.o

version:
	echo $(VERSION)
