# ONScripter-Jh-cmake
a cmake buildsystem version of ONScripter-Jh copy
only verified build under windows using msvc 2019
install vcpkg compile the Dependencies lib such as SDL2 SDL2_mixer etc.
modify vcpkge path in CMakeLists.txt
set(PKG_CONFIG_EXECUTABLE "D:/BuildTools/vcpkg/pkgconfig/bin/pkg-config")
set(CMAKE_TOOLCHAIN_FILE "D:/BuildTools/vcpkg/scripts/buildsystems/vcpkg.cmake")

little changes:
add screen scale options in command line
```
command onscripter -scale 1.5
```