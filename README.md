These are the instructions used to create the build wheels for pplx-kernels, DeepEP and DeepGEM using our native pixi environment.

Add these to the pixi environment
cuda-nvtx-dev
cuda-libraries-dev
libnvshmem-static
libnvshmem-dev

For pplx kernels - 
```
git clone https://github.com/perplexityai/pplx-kernels.git
cd pplx-kernels
CUDAARCHS="90-real" TORCH_CUDA_ARCH_LIST="9.0" CUDA_HOME=$CONDA_PREFIX/targets/x86_64-linux CUDA_TOOLKIT_ROOT=$CONDA_PREFIX/targets/x86_64-linux NCCL_HOME=$CONDA_PREFIX NVSHMEM_HOME=$CONDA_DIR CUDA_INCLUDE_DIRS=$CONDA_PREFIX/targets/x86_64-linux CUDA_PFX="$CONDA_PREFIX/targets/x86_64-linux" CMAKE_ARGS="-DCUDAToolkit_ROOT=$CUDA_PFX -DCUDA_TOOLKIT_ROOT_DIR=$CUDA_PFX -DCMAKE_CUDA_COMPILER=$CUDA_PFX/bin/nvcc -DCMAKE_PREFIX_PATH=$CUDA_PFX" python setup.py bdist_wheel
```

For DeepEp Kernels -
```
git clone https://github.com/deepseek-ai/DeepEP
cd DeepEP
CUDAARCHS="90-real" TORCH_CUDA_ARCH_LIST="9.0" CUDA_HOME=$CONDA_PREFIX/ CUDA_TOOLKIT_ROOT=$CONDA_PREFIX NCCL_HOME=$CONDA_PREFIX NVSHMEM_HOME=$CONDA_PREFIX CUDA_INCLUDE_DIRS=$CONDA_PREFIX/targets/x86_64-linux CUDA_PFX="$CONDA_PREFIX" CMAKE_ARGS="-DCUDAToolkit_ROOT=$CUDA_PFX -DCUDA_TOOLKIT_ROOT_DIR=$CUDA_PFX -DCMAKE_CUDA_COMPILER=$CUDA_PFX/bin/nvcc -DCMAKE_PREFIX_PATH=$CUDA_PFX" python setup.py bdist_wheel
```

For DeepGEM kernels -
Add this to the pixi environment
cutlass
Comment out the cutlass related imports from setup.py
```
git clone --recursive git@github.com:deepseek-ai/DeepGEMM.git
cd DeepGEM
touch scripts/__init__.py
PYTHONPATH=$PYTHONPATH:$(pwd) python setup.py bdist_wheel
```
