# Yojimbo Cmake
Cmake version of yojimbo. Please find the build instructions below.

## Mac
In order to build yojimbo with cmake you should download sodium and mbedtls
you can download this libraries using brew.

```
brew install libsodium
brew install mbedtls
```
After you installed the dependencies. You should clone the repository
```
git clone --recursive https://github.com/erdinckaya/yojimbo_cmake
mkdir build && cd build
cmake ..
make
```

## Windows
I strongly suggest to use [vcpkg](https://github.com/microsoft/vcpkg) to install dependencies you can use vcpkg for mac and linux as well.

```
vcpkg install libsodium:x64-windows
vcpkg install mbedtls:x64-windows
```
Now we can build our project. However you need toolchain path of vcpkg which you can find
it from [vcpkg](https://github.com/microsoft/vcpkg)'s github page.

```
git clone --recursive https://github.com/erdinckaya/yojimbo_cmake
mkdir build && cd build
cmake -DCMAKE_TOOLCHAIN_FILE=[vcpkg root]/scripts/buildsystems/vcpkg.cmake ..
make
```

PS: For further usage of yojimbo you can check this out [repo](https://github.com/erdinckaya/multiyer-pong) under mac branch.