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
        for cuver in cu92 cu101 cu102 cu110 ; do 
        NIGHTLIES_DATE=${torchver} PIP_UPLOAD_FOLDER="" TORCH_PACKAGE_NAME=torch PYTORCH_BRANCH=v${torchver} PYTORCH_BUILD_VERSION=${torchver}+${cuver} NIGHTLIES_ROOT_FOLDER=/mnt/nfliu/nightlies ./build_docker.sh  manywheel ${pyver} ${cuver} 2>&1 | tee /mnt/nfliu/nightlies/${torchver}.${pyver}.${cuver}.txt
        done 
    done
done
```

## PyTorch 1.7.1

``` sh
for torchver in 1.7.1 ; do 
    for pyver in 3.6m 3.7m 3.8 3.9 ; do 
        for cuver in cu92 cu101 cu102 cu110 ; do 
        NIGHTLIES_DATE=${torchver} PIP_UPLOAD_FOLDER="" TORCH_PACKAGE_NAME=torch PYTORCH_BRANCH=v${torchver} PYTORCH_BUILD_VERSION=${torchver}+${cuver} NIGHTLIES_ROOT_FOLDER=/mnt/nfliu/nightlies ./build_docker.sh  manywheel ${pyver} ${cuver} 2>&1 | tee /mnt/nfliu/nightlies/${torchver}.${pyver}.${cuver}.txt
        done 
    done
done
```
