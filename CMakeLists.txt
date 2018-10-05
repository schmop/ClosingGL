cmake_minimum_required (VERSION 3.8)

include(cmake/CMakeFunctions.txt)

#target_sources(CMakeProject1 INTERFACE ${lib})

include_directories(lib/include)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}")
SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}")

set(SOURCES src/main.cpp
    lib/include/GL/eglew.h
    lib/include/GL/glew.h
    lib/include/GL/glxew.h
    lib/include/GL/wglew.h
    lib/include/GLFW/glfw3.h
    lib/include/GLFW/glfw3native.h)

add_executable(CMakeProject1 ${SOURCES})

target_link_libraries(CMakeProject1 ${CMAKE_SOURCE_DIR}/lib/binary/glew32.lib)
target_link_libraries(CMakeProject1 OpenGL32)
target_link_libraries(CMakeProject1 ${CMAKE_SOURCE_DIR}/lib/binary/glfw3.lib)

add_custom_command(TARGET CMakeProject1 POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_SOURCE_DIR}/lib/binary/glew32.dll ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/glew32.dll)