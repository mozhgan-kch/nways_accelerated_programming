# Copyright (c) 2020 NVIDIA Corporation.  All rights reserved. 

FC := nvfortran
CC := nvc++

FLAGS := -O3 -w 
ACCFLAGS := -acc=multicore -Minfo=accel

NVTXLIB_F := -lnvhpcwrapnvtx

VER=$(shell nvc -dumpversion)
NVARCH=$(shell uname -s)_$(shell uname -m)
NVTXLIB_C := -I/opt/nvidia/hpc_sdk/$(NVARCH)/$(VER)/cuda/include

rdf_f: rdf.f90
	${FC} ${FLAGS} ${ACCFLAGS} -o rdf_f rdf.f90 ${NVTXLIB_F} 

rdf_c: rdf.cpp
	${CC} ${FLAGS} ${ACCFLAGS} -o rdf_c rdf.cpp ${NVTXLIB_C} 

clean:
	rm -f *.o rdf_f rdf_c
