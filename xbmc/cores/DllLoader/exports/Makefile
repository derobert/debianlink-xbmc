INCLUDES=-I. -I../../../ -I../../../linux -I../../../../guilib

SRCS=emu_dummy.cpp emu_dx8.cpp emu_kernel32.cpp exports_kernel32.cpp emu_msvcrt.cpp exports_msvcrt.cpp exports_python_linux.cpp wrapper.c

LIB=exports.a

include ../../../../Makefile.include
-include $(patsubst %.cpp,%.P,$(patsubst %.c,%.P,$(SRCS)))

wrapper.o : wrapper.c
	gcc -fPIC -c -g -D_LINUX -D_REENTRANT -D_LARGEFILE64_SOURCE -D_FILE_OFFSET_BITS=64 -D__USE_FILE_OFFSET64 $(INCLUDES) $< -o $@

exports_python_linux.o : exports_python_linux.cpp
	g++ -c -g -D_LINUX -D_REENTRANT -D_LARGEFILE64_SOURCE -D_FILE_OFFSET_BITS=64 -D__USE_FILE_OFFSET64 $(INCLUDES) $< -o $@

wrapper.def : wrapper.c
	(echo -n "-Wl"; grep __wrap wrapper.c | grep -v bash | sed "s/.*__wrap_//g" | sed "s/(.*//g" | awk '{printf(",-wrap,%s",$$0);}') > wrapper.def
