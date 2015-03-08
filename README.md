# Windows Installation
This is not the original [Caffe Readme](https://github.com/BVLC/caffe/blob/master/README.md) but an installation guide for windows version.

#### Want to run first before build by yourself?
You can download the windows x64 [standalone package](https://dl.dropboxusercontent.com/u/3466743/caffe-vs2012/standalone.7z) and run directly on MNIST dataset.

#### Prerequisites
You may need the followings to build the code:
- Windows 64-bit
- MS Visual Studio 2012
- CUDA toolkit 6.5
- Other dependencies which you can directly download from [here](http://dl.dropboxusercontent.com/u/3466743/caffe-vs2012/dependency-20140804.7z).

#### Build Steps
Currently it can be built by VS2012 for x64 flatform only. This is because the dependencies mentioned above is cross-compiled to support x64 only. If you want to build on 32bit windows, you need to rebuild your own 3rd-party libraries.
- Check out the code and switch to *windows* branch
- Download the dependency file and extract the folders inside to project root directory.
- Open the solution file in `./build/MSVC`
- Switch build target to x64 platform (Both debug and release are OK).
- If you CUDA installation directory is not `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v6.5\`, in the Solution Explorer right-click on `MainCaller -> Properties -> Configuration Properties -> Linker -> General -> Additional Library Directories` and add the path to the directory `lib\x64` inside your CUDA installation.
- Include any .cpp you want to build in the `./tools` directory to MainCaller.cpp.
- Build the code and you may find the `./bin/MainCaller.exe`

#### Train MNIST dataset
- Suppose you choose to build train_net.cpp which is the default one in MainCaller.cpp
- If you do not have GPU, please change it to CPU in `lenet_solver.prototxt`
- Goto directory `./examples/mnist`
- Double click `get_mnist_leveldb.bat` to download the dataset in leveldb format.
- Double click `train_lenet.bat` to see the training progress .

#### Tips
- It takes obvious longer time when you compile for the first time. Therefore please refrain from using `clean & rebuild`.
- To support different [GPU compute capabilities](http://en.wikipedia.org/wiki/CUDA#Supported_GPUs), the code is built for several compute capability versions. If you know the exact version of your GPU device, you may remove the support to other versions to speed up the compiling procedure. You may wish to take a look at #25 for more details.

#### Known Issues
- Because I am very busy doing my own project (may or may not be deep learning related), I am sorry that I do not have time to update the code to keep pace with the official Caffe development. As for the same reason, I will not be able to answer all the questions or solve the issues for some time.
- ~~I have trained on ImageNet with this windows porting as well. The speed is much slower than the one built on Ubuntu. 20 iterations take 79s on Windows, whereas same number of iterations take about 30s on Ubuntu (on GTX Titan).~~
- The above issue has been solved since the upgrade of GPU driver to 340.62 and CUDA to 6.5. The same hardware is now running 26 sencods for 20 iterations on Windows. Hooray!!

#### Bug Report
- Please create new issues in [github](https://github.com/niuzhiheng/caffe/issues) if you find any bug.
- If you have new pull requests, they are very welcome.
- Before you do that, you may wish to read this [wiki page](https://github.com/niuzhiheng/caffe/wiki) for more information.
