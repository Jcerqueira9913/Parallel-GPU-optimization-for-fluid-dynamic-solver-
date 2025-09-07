# Parallel GPU Optimization for Fluid Dynamic Solver

An optimized fluid solver originally implemented in C/C++ without parallelization.  
The code was restructured to leverage GPU acceleration and other performance improvements, reducing runtime from several **weeks** to just a few **seconds**.

---

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
