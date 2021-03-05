# pytorch builder

Scripts to build pytorch binaries and do end-to-end integration tests.

Folders:

- **conda** : files to build conda packages of pytorch, torchvision and other dependencies and repos
- **manywheel** : scripts to build linux wheels
- **wheel** : scripts to build OSX wheels
- **windows** : scripts to build Windows wheels
- **cron** : scripts to drive all of the above scripts across multiple configurations together
- **analytics** : scripts to pull wheel download count from our AWS s3 logs
- **test_community_repos** : scripts that test built binaries with various downstream repos that are high-priority and use pytorch
- **test_imports_docker** : some smoke tests to import torch in combination with other package imports, to check binary stability / compatibility

# Commands to build

## PyTorch 1.3.1

``` sh
for torchver in 1.3.1 ; do 
    for pyver in 3.5m 3.6m 3.7m ; do 
        for cuver in cu92 cu100 cu101 ; do 
        NIGHTLIES_DATE=${torchver} PIP_UPLOAD_FOLDER="" TORCH_PACKAGE_NAME=torch PYTORCH_BRANCH=v${torchver} PYTORCH_BUILD_VERSION=${torchver}+${cuver} NIGHTLIES_ROOT_FOLDER=/mnt/nfliu/nightlies ./build_docker.sh  manywheel ${pyver} ${cuver} 2>&1 | tee /mnt/nfliu/nightlies/${torchver}.${pyver}.${cuver}.txt 
        done
    done
done
```

## PyTorch 1.4.0

``` sh
for torchver in 1.4.0 ; do 
    for pyver in 3.5m 3.6m 3.7m 3.8 ; do 
        for cuver in cu92 cu100 cu101 ; do 
        NIGHTLIES_DATE=${torchver} PIP_UPLOAD_FOLDER="" TORCH_PACKAGE_NAME=torch PYTORCH_BRANCH=v${torchver} PYTORCH_BUILD_VERSION=${torchver}+${cuver} NIGHTLIES_ROOT_FOLDER=/mnt/nfliu/nightlies ./build_docker.sh  manywheel ${pyver} ${cuver} 2>&1 | tee /mnt/nfliu/nightlies/${torchver}.${pyver}.${cuver}.txt
        done 
    done
done
```

## PyTorch 1.5.0

``` sh
for torchver in 1.5.0 ; do 
    for pyver in 3.5m 3.6m 3.7m 3.8 ; do 
        for cuver in cu92 cu101 cu102 ; do 
        NIGHTLIES_DATE=${torchver} PIP_UPLOAD_FOLDER="" TORCH_PACKAGE_NAME=torch PYTORCH_BRANCH=v${torchver} PYTORCH_BUILD_VERSION=${torchver}+${cuver} NIGHTLIES_ROOT_FOLDER=/mnt/nfliu/nightlies ./build_docker.sh  manywheel ${pyver} ${cuver} 2>&1 | tee /mnt/nfliu/nightlies/${torchver}.${pyver}.${cuver}.txt
        done 
    done
done
```

## PyTorch 1.5.1

``` sh
for torchver in 1.5.1 ; do 
    for pyver in 3.5m 3.6m 3.7m 3.8 ; do 
        for cuver in cu92 cu101 cu102 ; do 
        NIGHTLIES_DATE=${torchver} PIP_UPLOAD_FOLDER="" TORCH_PACKAGE_NAME=torch PYTORCH_BRANCH=v${torchver} PYTORCH_BUILD_VERSION=${torchver}+${cuver} NIGHTLIES_ROOT_FOLDER=/mnt/nfliu/nightlies ./build_docker.sh  manywheel ${pyver} ${cuver} 2>&1 | tee /mnt/nfliu/nightlies/${torchver}.${pyver}.${cuver}.txt
        done 
    done
done
```

## PyTorch 1.6.0

``` sh
for torchver in 1.6.0 ; do 
    for pyver in 3.6m 3.7m 3.8 ; do 
        for cuver in cu92 cu101 cu102 ; do 
        NIGHTLIES_DATE=${torchver} PIP_UPLOAD_FOLDER="" TORCH_PACKAGE_NAME=torch PYTORCH_BRANCH=v${torchver} PYTORCH_BUILD_VERSION=${torchver}+${cuver} NIGHTLIES_ROOT_FOLDER=/mnt/nfliu/nightlies ./build_docker.sh  manywheel ${pyver} ${cuver} 2>&1 | tee /mnt/nfliu/nightlies/${torchver}.${pyver}.${cuver}.txt
        done 
    done
done
```

## PyTorch 1.7.0

``` sh
for torchver in 1.7.0 ; do 
    for pyver in 3.6m 3.7m 3.8 ; do 
        # See caveats for why we can't buld cu110
        for cuver in cu92 cu101 cu102 ; do 
        NIGHTLIES_DATE=${torchver} PIP_UPLOAD_FOLDER="" TORCH_PACKAGE_NAME=torch PYTORCH_BRANCH=v${torchver} PYTORCH_BUILD_VERSION=${torchver}+${cuver} NIGHTLIES_ROOT_FOLDER=/mnt/nfliu/nightlies ./build_docker.sh  manywheel ${pyver} ${cuver} 2>&1 | tee /mnt/nfliu/nightlies/${torchver}.${pyver}.${cuver}.txt
        done 
    done
done
```

## PyTorch 1.7.1

``` sh
for torchver in 1.7.1 ; do 
    for pyver in 3.6m 3.7m 3.8 3.9 ; do 
        # See caveats for why we can't buld cu110
        for cuver in cu92 cu101 cu102 ; do 
        NIGHTLIES_DATE=${torchver} PIP_UPLOAD_FOLDER="" TORCH_PACKAGE_NAME=torch PYTORCH_BRANCH=v${torchver} PYTORCH_BUILD_VERSION=${torchver}+${cuver} NIGHTLIES_ROOT_FOLDER=/mnt/nfliu/nightlies ./build_docker.sh  manywheel ${pyver} ${cuver} 2>&1 | tee /mnt/nfliu/nightlies/${torchver}.${pyver}.${cuver}.txt
        done 
    done
done
```

# Caveats

## PyTorch 1.7.0 and 1.7.1 CUDA 11.0 Builds

Unfortunately, I wasn't able to build binaries for PyTorch 1.7.0 or 1.7.1 on CUDA 11.0 . When doing so, you run into the following error:

``` 
[ 86%] Linking CXX shared library ../lib/libtorch_cuda.so
CMakeFiles/torch_cuda.dir/__/aten/src/ATen/native/cudnn/AffineGridGenerator.cpp.o: In function `_GLOBAL
__sub_I_AffineGridGenerator.cpp':
AffineGridGenerator.cpp:(.text.startup+0x3): relocation truncated to fit: R_X86_64_PC32 against `.bss'
AffineGridGenerator.cpp:(.text.startup+0x21): relocation truncated to fit: R_X86_64_PC32 against `.bss'
CMakeFiles/torch_cuda.dir/__/aten/src/ATen/native/cudnn/RNN.cpp.o: In function `at::native::(anonymous
namespace)::get_dropout_state(double, bool, c10::TensorOptions)':
RNN.cpp:(.text+0x1aec): relocation truncated to fit: R_X86_64_PC32 against `.bss'
RNN.cpp:(.text+0x1af7): relocation truncated to fit: R_X86_64_PC32 against `.bss'
RNN.cpp:(.text+0x1b17): relocation truncated to fit: R_X86_64_PC32 against `.bss'
RNN.cpp:(.text+0x1b3e): relocation truncated to fit: R_X86_64_PC32 against `.bss'
RNN.cpp:(.text+0x1b45): relocation truncated to fit: R_X86_64_PC32 against `.bss'
RNN.cpp:(.text+0x1bcc): relocation truncated to fit: R_X86_64_PC32 against `.bss'
RNN.cpp:(.text+0x1bd7): relocation truncated to fit: R_X86_64_PC32 against `.bss'
RNN.cpp:(.text+0x1be5): relocation truncated to fit: R_X86_64_PC32 against `.bss'
RNN.cpp:(.text+0x1c21): additional relocation overflows omitted from the output
collect2: error: ld returned 1 exit status
gmake[2]: *** [lib/libtorch_cuda.so] Error 1
gmake[1]: *** [caffe2/CMakeFiles/torch_cuda.dir/all] Error 2
gmake: *** [all] Error 2
```

This is due to https://github.com/pytorch/pytorch/issues/39968 , which was not fixed until `1.8.0` .
