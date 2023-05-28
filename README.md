# SanitizerPlayground

Collection of test code to play with gcc sanitizers. Taken from [RedHat](https://developers.redhat.com/blog/2021/05/05/memory-error-checking-in-c-and-c-comparing-sanitizers-and-valgrind)

## Motivation

I needed same sample output to write parsers for GCC sanitizer results. The above webpage provided the required test cases.

## Build (Linux)

```
git clone https://github.com/ukoehler/SanitizerPlayground.git
cd SanitizerPlayground
mkdir build
cd build
```

Either 
```
cmake -DCMAKE_BUILD_TYPE=Debug -DAddressSanitize=ON ..
```
or
```
cmake -DCMAKE_BUILD_TYPE=Debug -DThreadSanitize=ON ..
```

followed by
```
make
```

## Run examples 

Follow above with
```
cd src
./global
./leak
./overrun
./stack
./tiny
./uar
./undefined
./uninit
```