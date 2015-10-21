cmake_minimum_required(VERSION 2.8)
project (bibnumber)

# c++11 required
include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)

if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
else()
    message(STATUS "The compiler ${CMAKE_CXX_COMPILER} doesn’t support C++11. Please upgrade or use a different C++ compiler.")
endif()

# opencv package required
find_package(OpenCV REQUIRED)
find_package(Boost COMPONENTS filesystem system REQUIRED)

# easypr library
include_directories(.)
set(SOURCE_FILES
    bibnumber.cpp
    batch.cpp
    facedetection.cpp
    log.cpp
    pipeline.cpp
    textdetection.cpp
    textrecognition.cpp
    train.cpp
)
#add_library(bibnumber STATIC ${SOURCE_FILES})

# test cases
add_executable(bibnumber ${SOURCE_FILES})

target_link_libraries(bibnumber ${OpenCV_LIBS} ${Boost_LIBRARIES} lept tesseract)
