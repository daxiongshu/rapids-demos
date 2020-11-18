# rapids-demos

### Introduction

In this demo, we show an end-to-end workflow of rapids `dask-cudf` + [`dask-glm`](https://github.com/dask/dask-glm) ([doc](https://ml.dask.org/glm.html)) `LogisticRegression` on mutliple GPUs. 
Experiments are done on a `DGX-1` with `8xGPUs` and `40-core CPUs`. 
With the HIGGS dataset, the GPU solution achieves **14x speedup** over CPU using the **lbfgs** solver. 
To get a more comprehensive speedup measurement, we run `dask-glm` on vared sizes of random synthetic data and the GPU solution achieves up to **27x speedup** over CPU.

### Background

**Multi-GPU support of dask-glm is enabled by recent efforts of allowing cupy dask arrays as inputs.** [dask/dask-glm#87](https://github.com/dask/dask-glm/pull/87) and [dask/dask-glm#89](https://github.com/dask/dask-glm/pull/89)

dask-glm offers 3 estimators:
- LinearRegression
- LogisticRegression
- PoissonRegression

and 5 solvers:
- admm,
- gradient_descent,
- newton,
- lbfgs,
- proximal_grad

Currently, all 3 estimators and 5 algorithms work seamlessly with `dask cupy arrays` and `dask-cudf` on multiple GPUs. 


### Install instructions:

- conda create -n rapids-0.17 -c rapidsai-nightly -c nvidia -c conda-forge -c defaults rapids=0.17 python=3.7 cudatoolkit=10.2
- conda activate rapids-0.17    
- pip install git+https://github.com/dask/dask
- pip install matplotlib
- git clone https://github.com/dask/dask-glm
- cd dask-glm
- pip install -e .
