# Copyright (c) 2017-2018, NVIDIA CORPORATION. All rights reserved.
NVCC=nvcc
#CUDA_HOME=hpc_sdk_path/Linux_x86_64/21.3/cuda/11.2/
GENCODE_SM60    := -gencode arch=compute_60,code=sm_60
GENCODE_SM70    := -gencode arch=compute_70,code=sm_70
GENCODE_SM80    := -gencode arch=compute_80,code=sm_80 -gencode arch=compute_80,code=compute_80
GENCODE_SM90    := -gencode arch=compute_90,code=sm_90 -gencode arch=compute_90,code=compute_90
GENCODE_FLAGS	:= $(GENCODE_SM70) $(GENCODE_SM80) $(GENCODE_SM90)
ifdef DISABLE_CUB
        NVCC_FLAGS = -Xptxas --optimize-float-atomics
else
        NVCC_FLAGS = -DHAVE_CUB
endif
NVCC_FLAGS += -Xcompiler -fopenmp -lineinfo -DUSE_NVTX -lnvToolsExt $(GENCODE_FLAGS) -std=c++14
jacobi: Makefile jacobi.cu
	$(NVCC) $(NVCC_FLAGS) jacobi.cu -o jacobi

.PHONY.: clean
clean:
	rm -f jacobi jacobi_report.nsys-rep

sanitize: jacobi
	compute-sanitizer ./jacobi -niter 10

run: jacobi
	./jacobi

profile: jacobi
	nsys profile --trace=cuda,nvtx -o jacobi ./jacobi -niter 10
