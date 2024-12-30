# cmake-glslang
A CMake utility for compiling shaders to SPIRV using glslang.

## Usage

### CMake
```cmake
include(FetchContent)
FetchContent_Declare(cmake-glslang
  GIT_REPOSITORY https://github.com/antlilja/cmake-glslang.git
  GIT_TAG SOME_GIT_HASH
)
FetchContent_MakeAvailable(cmake-glslang)

compile_glsl_shaders(SHADER_FILES "shaders/triangle.vert" "shaders/triangle.frag")

...
```
