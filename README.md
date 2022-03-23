# Basic Profiling Application with CMake
## _using Google Perf Tools_


First step is to install google-perftools Package on Ubuntu:
```sh
sudo apt-get update –y
sudo apt-get install -y google-perftools libgoogle-perftools-dev
```
We should create a build directory
```sh
mkdir build
cd build
cmake ..
```

After that we would like to implement codemodel-v2
```sh
cd build
mkdir -p .cmake/api/v1/query
touch .cmake/api/v1/query/codemodel-v2
cmake ..
```
After we run cmake, the codemodel .json files are being generated in .cmake/api/v1/reply

Now we can start using Google Perf tools
```sh
make -j LDFLAGS="-all-static -lprofiler"
LD_PRELOAD=/usr/lib/libprofiler.so CPUPROFILE=<name>.prof CPUPROFILE_FREQUENCY=100000 ./<outputname>
google-pprof ./<outputname> <name>.prof
```
libprofiler.so might also be in /usr/lib/x86_64-linux-gnu  
We can also generate a pdf with cpuprofile info:
```sh
google-pprof --pdf ./<outputname> <name>.prof > <name>.pdf
```
