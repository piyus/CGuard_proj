
Welcome to the CGuard repository.  


# Clone project repository:  
git clone https://github.com/piyus/CGuard_proj.git  
cd CGuard_proj  
git submodule update --remote --merge --init  

# Install dependencies:  
sh resources/dependency.sh  


# Building CGuard:  

# To compile CGuard and run Phoenix follow the steps below  
cp resources/cg.sh .  
./cg.sh  


# To see the phoenix results  
cd cg/Phoenix-2.0_cg/logs  
sh phoenix1.sh  
It will print all the results on the console.  


# To run the basic examples (from CGuard_proj)  
cd examples  
make  
make good  
make bad  

# To compile a program test.c using CGuard, use the following command  
path-to-CGuard_proj/build/bin/clang -fsanitize=fastaddress -O3 test.c -L path-to-CGuard_proj/jemalloc/lib -ljemalloc_cg -lsupport  
To run the program compiled using CGuard, use the following command  
LD_LIBRARY_PATH=path-to-CGuard_proj/jemalloc/lib ./a.out  

# SPEC  
For SPEC you need to purchase SPEC 2017 that contains cpu2017-1_0_5.iso  

# Running SPEC using CGuard (from CGuard_proj)  
Set BASE_DIR at line-198 in resources/cg.cfg to path-to-CGuard_proj  
mkdir -p tmp  
cd -p tmp  
ln -s path-to-cpu2017-1_0_5.iso .  
cp ../resources/spec_cg.sh .  
chmod +x spec_cg.sh  
./spec_cg.sh  


# To compile Native and run Phoenix follow the steps below  
mkdir native  
cd native  
cp ../resources/native.sh .  
./native.sh  

# To see the phoenix results  
cd Phoenix-2.0_cg/logs  
sh phoenix1.sh  
It will print all the results on the console.  

# Running SPEC for native (from CGuard_proj/native)  
Set BASE_DIR at line-198 in ../../resources/native.cfg to path-to-CGuard_proj  
mkdir tmp1  
cd tmp1  
ln -s path-to-cpu2017-1_0_5.iso .  
cp ../../resources/spec.sh .  
chmod +x spec.sh  
./spec.sh  


# Below are the steps that cg.sh follows  
mkdir build  
cd build  
cp ../resources/build.sh .  
sh build.sh  
ninja  

It will take a while to compile llvm.  

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

# steps followed to run Phoenix using CGuard  
git clone https://github.com/piyus/Phoenix-2.0_cg  
cd Phoenix-2.0_cg/input  
sh download.sh  

It will download the test input files.  

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

Thanks for using our tool.

References:
CGuard: Scalable and Precise Object Bounds Protection for C (ISSTA-2023)
