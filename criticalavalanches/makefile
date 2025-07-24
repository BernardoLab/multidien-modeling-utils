# CC=g++
# CFLAGS = -std=c++11 -O3 -Wno-unused-result -DNDEBUG
# # adjust path to find hdf5, for example:
# IFLAGS = -L /usr/local/lib -L /usr/lib/x86_64-linux-gnu/hdf5/serial -I /usr/local/include -I /usr/include/hdf5/serial -I ./src/
# LFLAGS = -lstdc++ -lz -lhdf5

# all: cc cc_orlandi cc_random

# more: nocc nocc_orlandi nocc_random

#––– Compiler and flags
CC      := g++
CFLAGS  := -std=c++11 -O3 -Wno-unused-result -DNDEBUG

#––– Homebrew‐installed HDF5 prefix
HDF5_PREFIX := $(shell brew --prefix hdf5)

#––– Include and library paths
#  -I for headers, -L for libs
IFLAGS := -I$(HDF5_PREFIX)/include -I./src
LFLAGS := -L$(HDF5_PREFIX)/lib -lhdf5 -lz -lstdc++

#––– Targets
all: cc cc_orlandi cc_random

more: nocc nocc_orlandi nocc_random

#––– Build rule for your main executable
exe/cc: src/main.cpp src/helper_io.hpp
	$(CC) $(CFLAGS) $(IFLAGS) $< -o $@ $(LFLAGS)

# (repeat or pattern‐rule for cc_orlandi, cc_random, etc.)


# default (coalesence compensated) local gauss branching network
cc: ./src/main.cpp
	@mkdir -p ./exe
	$(CC) $(CFLAGS) $(IFLAGS) -DTPGAUSS ./src/main.cpp -o ./exe/cc $(LFLAGS)

# disables coalesence compensation
nocc: ./src/main.cpp
	@mkdir -p ./exe
	$(CC) $(CFLAGS) $(IFLAGS) -DNOCC -DTPGAUSS  ./src/main.cpp -o ./exe/nocc $(LFLAGS)

# orlandi topology
cc_orlandi: ./src/main.cpp
	@mkdir -p ./exe
	$(CC) $(CFLAGS) $(IFLAGS) -DTPORLANDI ./src/main.cpp -o ./exe/cc_orlandi $(LFLAGS)

nocc_orlandi: ./src/main.cpp
	@mkdir -p ./exe
	$(CC) $(CFLAGS) $(IFLAGS) -DNOCC -DTPORLANDI ./src/main.cpp -o ./exe/nocc_orlandi $(LFLAGS)

# random graph topology.
cc_random: ./src/main.cpp
	@mkdir -p ./exe
	$(CC) $(CFLAGS) $(IFLAGS) -DTPRANDOM ./src/main.cpp -o ./exe/cc_random $(LFLAGS)

nocc_random: ./src/main.cpp
	@mkdir -p ./exe
	$(CC) $(CFLAGS) $(IFLAGS) -DNOCC -DTPRANDOM ./src/main.cpp -o ./exe/nocc_random $(LFLAGS)

clean:
	@rm -rf ./exe/*
