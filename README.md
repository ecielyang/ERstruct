# ERstruct - Official Python Implementation

A Python package for inferring the number of top informative PCs that capture population structure based on genotype information.

## Requirements for Data File
Data files must be of .npy format. The data matrix must with 0,1,2 and/or NaN (for missing values) entries only, the rows represent individuals and columns represent markers. If there are more than one data files, the data matrix inside must with the same number of rows.

## Dependencies
ERStruct depends on `numpy`, `torch` and `joblib`.

## Installation
Users can install `ERStruct` by running the command below in command line:
```commandline
pip install ERStruct
```

Import the module
```
from ERStruct import erstruct
```
## Parameters
```
erstruct(n, path, filename, rep, alpha, cpu_num=1, device_idx="cpu", varm=1, Kc=-1)
```

**n** *(int)* - total number of individuals in the study

**path** *(str)* - The path of data file(s)

**filename** *(list)*: The name of the data file(s)

**rep** *(int)*: Number of simulation times for the null distribution

**alpha** *(float)*: Significance level, can be either a scaler or a vector

**Kc** *(int)*: A coarse estimate of the top PCs number (set to `-1` by default)

**core_num** *(int)*: Optional, number of CPU cores to be used for parallel computing. The default is 1

**device_idx** *(str)*: "cpu" pr "gpu". The default is "cpu".

**varm** *(iny)*: Allocated memory (in bytes) of GPUs for computing. When device_idx="cpu", varm should be specified clearly.

## Examples
Run the code on CPUs:
```commandline
test = erstruct(2504, '.', ['test_chr21', 'test_chr22'], 5000, 1e-4, cpu_num=1, device_idx="cpu")
K = test.run()
```
Run the code on GPUs:
```commandline
test = erstruct(2504, '.', ['test_chr21', 'test_chr22'], 5000, 1e-4, device_idx="gpu", varm=12000000000)
K = test.run()
```
Example data files `test_chr21.npy` and `test_chr22.npy` can be found on the "sample_data" of [ERStruct GitHub repository](https://github.com/ecielyang/ERStruct).




## Other Details
Please refer to our paper
> *An Eigenvalue Ratio Approach to Inferring Population Structure from Whole Genome Sequencing Data*.