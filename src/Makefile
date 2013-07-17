C++ = g++

ifndef os
   os = LINUX
endif

ifndef arch
   arch = IA32
endif

CCFLAGS = -Wall -D$(os) -I../udt/src -finline-functions -g

ifeq ($(arch), IA32)
   CCFLAGS += -DIA32 #-mcpu=pentiumpro -march=pentiumpro -mmmx -msse
endif

ifeq ($(arch), POWERPC)
   CCFLAGS += -mcpu=powerpc
endif

ifeq ($(arch), IA64)
   CCFLAGS += -DIA64
endif

ifeq ($(arch), SPARC)
   CCFLAGS += -DSPARC
endif

LDFLAGS = -L../src ../udt/src/libudt.a -lstdc++ -lpthread -lm -lssl -lcrypto

ifeq ($(os), UNIX)
   LDFLAGS += -lsocket
endif

ifeq ($(os), SUNOS)
   LDFLAGS += -lrt -lsocket
endif

DIR = $(shell pwd)

APP = udtcat  #test


all: $(APP)

%.o: %.cpp 
	$(C++) $(CCFLAGS) $< -c

udtcat: udtcat.o udtcat_threads.o udtcat_server.o udtcat_client.o
	$(C++) $^ -o $@ $(LDFLAGS)

clean:
	rm -f *.o $(APP)

install:
	export PATH=$(DIR):$$PATH