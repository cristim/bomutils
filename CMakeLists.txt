cmake_minimum_required(VERSION 3.13)
project(bomutils CXX)

if(DARLING)
    include(darling_exe)

    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -nostdinc")
    foreach(tool mkbom lsbom)
        add_darling_executable(${tool}
            src/${tool}.cpp
            src/printnode.cpp
            src/crc32.cpp)
        target_compile_features(${tool} PRIVATE cxx_std_11)
        target_link_libraries(${tool} cxx)
        install(TARGETS ${tool} DESTINATION libexec/darling/usr/bin)
    endforeach()
endif()
