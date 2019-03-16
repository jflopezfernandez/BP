
vpath %.cpp src
vpath %.hpp include

.SUFFIXES:
.SUFFIXES: .cpp .hpp

SHELL    = /bin/sh

OPTIMIZATIONS = -falias -fast -m64 -mtune=core-avx2 -masm=intel -fno-rtti -fstrict-aliasing -funroll-loops 
CPPFLAGS = -I include
CC       = icc
CFLAGS   = -std=c11 $(OPTIMIZATIONS)
CXX      = icpc
CXXFLAGS = -std=c++17 $(OPTIMIZATIONS)

BOOST_PROGRAM_OPTIONS     = -lboost_program_options
BOOST_LIBS = $(BOOST_PROGRAM_OPTIONS)
INTEL_LIBS = -L $(MKLPATH)/lib/intel64_lin -lmkl_intel_lp64 -lmkl_sequential -lmkl_core -lpthread -lm
INCLUDE_DIRECTORIES = -I $(MKLINCLUDEDIR)
ADDITIONAL_LIBS = $(BOOST_LIBS) $(INTEL_LIBS)

SRCS     = Bpp.cpp Options.cpp Monomers.cpp
OBJS     = $(patsubst %.cpp, %.o, $(SRCS))
PROGRAM   = bpp

OUTPUT_OPTION = -o $@
COMPILE.cpp = $(CXX) $(CXXFLAGS) $(CPPFLAGS) $(TARGET_ARCH) -c
LINK.o = $(CXX) $(LDFLAGS) $(TARGET_ARCH)

all: $(PROGRAM)

$(TARGET):	$(OBJS)
	$(LINK.o) $(OUTPUT_OPTION) $^ $(LIBS) $(ADDITIONAL_LIBS)

%.o: %.cpp 
	$(COMPILE.cpp) $(OUTPUT_OPTION) $^

.PHONY: clean
clean:
	$(RM) $(OBJS) $(TARGET) output.txt
