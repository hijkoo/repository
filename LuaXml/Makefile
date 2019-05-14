# generic compiler and linker settings:
CC     = gcc
INCDIR = -I/home/pubsrv/openresty/luajit/include/luajit-2.1
LIB    =
LIBDIR =  -L. -L/home/pubsrv/openresty/luajit/lib


CFLAGS = -Os -Wall -c #-g

# generic platform specific rules:
ARCH            = $(shell uname -s)
ifeq ($(ARCH),Linux)
  CFLAGS += -fPIC
  LFLAGS =  -fPIC -shared
  LIBS          = $(LIBDIR) $(LIB) -lluajit-5.1 -ldl
  EXESUFFIX =
  SHLIBSUFFIX = .so

else
  ifeq ($(ARCH),Darwin) # MacOSX
    LFLAGS = -bundle
    LIBS          = $(LIBDIR) -L/usr/local/lib $(LIB) -lluajit-5.1
    EXESUFFIX = .app
    SHLIBSUFFIX = .so

  else  # windows, MinGW
    LFLAGS =  -shared
    LIBS          = $(LIBDIR) $(LIB) -llua51 -mconsole -s
    EXESUFFIX = .exe
    SHLIBSUFFIX = .dll

  endif
endif

# project specific targets:
all:  LuaXML_lib$(SHLIBSUFFIX)

# project specific link rules:
LuaXML_lib$(SHLIBSUFFIX): LuaXML_lib.o
        $(CC) -o $@ $(LFLAGS) $^ $(LIBS)

# project specific dependencies:
LuaXML_lib.o:  LuaXML_lib.c

# generic rules and targets:
.c.o:
        $(CC) $(CFLAGS) $(INCDIR) -c $<
clean:
        rm -f *.o *~ LuaXML_lib.so LuaXML_lib.dll

