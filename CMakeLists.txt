include(FetchContent)
FetchContent_Declare(glslang
  GIT_REPOSITORY https://github.com/KhronosGroup/glslang.git
  GIT_TAG 15.0.0
)
set(ENABLE_OPT OFF)
set(ENABLE_HLSL OFF)
FetchContent_MakeAvailable(glslang)

function(compile_glsl_shaders out_files)
  set(result)
  foreach(in_file ${ARGN})
    set(out_file "${CMAKE_CURRENT_BINARY_DIR}/shaders/${in_file}.spv")
    get_filename_component(out_file_dir "${out_file}" DIRECTORY)
    add_custom_command(
      OUTPUT ${out_file}
      COMMAND ${CMAKE_COMMAND} -E make_directory "${out_file_dir}"
      COMMAND glslang-standalone -V -o "${out_file}" "${in_file}"
      DEPENDS glslang-standalone "${in_file}"
      WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
      COMMENT "Building glsl shader ${in_file}"
      VERBATIM)
    list(APPEND result "${out_file}")
  endforeach()
  set(${out_files} "${result}" PARENT_SCOPE)
endfunction()
