
Welcome to the CGuard repository.

Building CGuard:

Clone the project repository:
git clone https://github.com/piyus/CGuard_proj.git
cd CGuard_proj
git submodule update --init

Install dependencies:
sh resources/dependency.sh


mkdir build
cd build
cp ../resources/build.sh .
sh build.sh
ninja

It will take a while.

cd ..
cd jemalloc
sh autogen.sh
make -j

Now we are ready to run the basic examples
cd ..
cd examples
make
make good
make bad

cd ..

To run Phoenix using CGuard clone Phoenix in the CGuard_proj folder
git clone https://github.com/piyus/Phoenix-2.0_cg
cd Phoenix-2.0_cg/input
sh download.sh

It will download the input files.

cd ..
source setenv.sh

This will set some environment variables.

make
cd tests
sh run.sh

It will take a while to run all benchmarks.

cd ..
cd logs
sh phoenix1.sh

It will print all the results.


To compile a program test.c using CGuard, use the following command
path-to-CGuard_proj/build/bin/clang -fsanitize=fastaddress -O3 test.c -L path-to-CGuard_proj/jemalloc/lib -ljemalloc_cg -lsupport
To run the program compiled using CGuard, use the following command
LD_LIBRARY_PATH=path-to-CGuard_proj/jemalloc/lib ./a.out

To run SPEC benchmarks:
Use resources/default.cfg configuration.
Set BASE_DIR variable in default.cfg to path-to-CGuard_proj
