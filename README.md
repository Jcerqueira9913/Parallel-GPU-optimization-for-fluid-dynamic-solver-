# Parallel GPU Optimization for Fluid Dynamic Solver

An optimized fluid solver originally implemented in C/C++ without parallelization.  
The code was restructured to leverage GPU acceleration and other performance improvements, reducing runtime from several **weeks** to just a few **seconds**.

---
## 📄 Supporting Report

At the root of this repository, there is a PDF file containing a detailed report in **Portuguese**.  
The report explains and justifies the entire GPU optimization process, including the modifications made to the original C/C++ code, performance improvements, and the testing methodology.  
It also includes instructions on how to implement an OpenMP optimization on the original code.  
The original code is available at [3DFluid GitHub repository](https://github.com/BlainMaguire/3dfluid).


## 📂 Where is the code?

The main implementation is located in the `.cu` files:  

- `main.cu` – entry point of the program  
- `fluid_solver.cu` – GPU-optimized fluid solver  
- `EventManager.cpp` – event handling utilities  

---

## ⚙️ Requirements

To build and run the solver you will need:  

- **gcc** (GNU Compiler Collection)  
- **nvcc** (NVIDIA CUDA Compiler)  
- An **NVIDIA GPU** compatible with your chosen CUDA architecture  

---

## 🚀 How to Build and Run

Inside the `src/` directory there is a `Makefile`.  
By default, it compiles the solver with the following command:  

```bash
nvcc -O3 -arch=sm_35 -Wno-deprecated-gpu-targets -use_fast_math -maxrregcount=32 main.cu fluid_solver.cu EventManager.cpp -o fluid_sim
```
> ⚠️ Note: The flags can be modified depending on your GPU model. The provided configuration is tuned for NVIDIA Kepler GPUs.  

### Run locally

On Linux, you can run:

```bash
./fluid_sim
```
If you want to check execution time:

```bash
time ./fluid_sim
```

### Run on SLURM

The Makefile also includes a target to submit jobs via SLURM. Use:

```bash
make run
```
This will call the run.sh script with sbatch.

## 🧹 Cleaning Up

To remove the compiled binary and clean the project, run:

```bash
make clean
```
This will delete the fluid_sim executable and any temporary build files.

## 📌 Notes

- The project was migrated from a sequential CPU version to a massively parallel GPU version.  
- Performance gain: **weeks → seconds** depending on the simulation size and GPU hardware.  
- CUDA compiler flags (`-O3 -arch=sm_35 -use_fast_math -maxrregcount=32`) can be adjusted for different GPU architectures to achieve optimal performance.  
- The project includes a Makefile that simplifies compilation and execution, including support for SLURM job submission.  
