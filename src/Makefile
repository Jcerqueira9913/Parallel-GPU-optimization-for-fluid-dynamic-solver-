CPP = nvcc -O3 -arch=sm_35 -Wno-deprecated-gpu-targets -use_fast_math -maxrregcount=32

SRCS = main.cu fluid_solver.cu EventManager.cpp

all:
	$(CPP) $(SRCS) -o fluid_sim

clean:
	@echo Cleaning up...
	@rm fluid_sim
	@echo Done.

run:
	sbatch run.sh

.PHONY: run