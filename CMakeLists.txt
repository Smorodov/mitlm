cmake_minimum_required(VERSION 3.0)

project(mitlm VERSION 0.2)

set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/build)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})

set(CMAKE_DEBUG_POSTFIX _d)
set(CMAKE_CXX_STANDARD 11)

add_subdirectory(libf2c)

add_definitions(-DUNICODE -D_UNICODE)

set( UTIL_SOURCES 
src/util/RefCounter.cpp
src/util/Logger.cpp
src/util/CommandOptions.cpp)

set(SOURCES ${UTIL_SOURCES}
    "${CMAKE_SOURCE_DIR}/src/Vocab.cpp"
    "${CMAKE_SOURCE_DIR}/src/NgramVector.cpp"
    "${CMAKE_SOURCE_DIR}/src/NgramModel.cpp"
    "${CMAKE_SOURCE_DIR}/src/NgramLM.cpp"
    "${CMAKE_SOURCE_DIR}/src/InterpolatedNgramLM.cpp"
    "${CMAKE_SOURCE_DIR}/src/Smoothing.cpp"
    "${CMAKE_SOURCE_DIR}/src/MaxLikelihoodSmoothing.cpp"
    "${CMAKE_SOURCE_DIR}/src/KneserNeySmoothing.cpp"
    "${CMAKE_SOURCE_DIR}/src/PerplexityOptimizer.cpp"
    "${CMAKE_SOURCE_DIR}/src/WordErrorRateOptimizer.cpp"
    "${CMAKE_SOURCE_DIR}/src/Lattice.cpp" 

    "${CMAKE_SOURCE_DIR}/src/optimize/lbfgs_f2c.c" 
    "${CMAKE_SOURCE_DIR}/src/optimize/lbfgsb_f2c.c"
    "${CMAKE_SOURCE_DIR}/src/optimize/fortran_wrapper.c"
)

include_directories("${CMAKE_SOURCE_DIR}/src")
add_library(libmitlm STATIC ${HEADERS} ${SOURCES})
target_link_libraries(libmitlm libf2c)
# estimate-ngram interpolate-ngram evaluate-ngra

add_executable(estimate-ngram src/estimate-ngram.cpp)
target_link_libraries(estimate-ngram libmitlm )
add_executable(interpolate-ngram src/interpolate-ngram.cpp)
target_link_libraries(interpolate-ngram libmitlm)
add_executable(evaluate-ngram src/evaluate-ngram.cpp)
target_link_libraries(evaluate-ngram libmitlm)
