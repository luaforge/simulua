CC = gcc
CFLAGS = -W -Wall -pedantic -O2

# Linux
INCFLAGS = -I/usr/include/lua5.1
LUALIB = /usr/lib/liblua5.1.a
LUACFLAGS = -DLUA_USE_LINUX
LIBS = -lm -Wl,-E -ldl -lreadline -lhistory -lncurses
# MacOSX
#INCFLAGS = -I/sw/include
#LUALIB = /sw/lib/liblua.a
#LUACFLAGS = -DLUA_USE_LINUX
#LIBS = -lm -lreadline

RM = rm -f
LUAC = luac
HEX = xxd -i

LIBOBJS = rng.o ranlib.o mt.o cdf.o dcdflib.o ipmpar.o \
			 binomial.o queue.o stack.o
OBJS = slinit.o simulua.o

BIN = simulua
LUA = ../simulua.lua
LC = simulua.lc
INC = simulua_lc.h

all : $(BIN)

$(BIN) : $(INC) $(OBJS) $(LIBOBJS)
	$(CC) $(CFLAGS) $(INCFLAGS) -o $@ $^ $(LUALIB) $(LIBS)

$(INC) : $(LC)
	$(HEX) $< > $@

$(LC) : $(LUA)
	$(LUAC) -o $@ $<

$(LIBOBJS) : %.o : ../lib/%.c
	$(CC) $(CFLAGS) $(INCFLAGS) -c -o $@ $<

$(OBJS) : %.o : %.c
	$(CC) $(CFLAGS) $(LUACFLAGS) $(INCFLAGS) -c -o $@ $<

clean :
	$(RM) $(LIBOBJS) $(OBJS) $(BIN) $(LC) $(INC)
