# Local libraries
include_directories(../modules/CvGl)
include_directories(../modules/PoseExpr/include)
add_definitions(-std=c++11)
add_definitions(-DDLIB_JPEG_SUPPORT)
add_definitions(-DDLIB_PNG_SUPPORT)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")
set(CMAKE_BUILD_TYPE Release)
SET(SOURCE
    ../main.cpp
)

SET(CMAKE_CXX_FLAGS "-w -fopenmp")
add_executable(TestBump ${SOURCE})

if(WIN32)
	target_link_libraries(TestBump ${OpenCVLibraries})
endif(WIN32)
if(UNIX)
	target_link_libraries(TestBump ${OpenCV_LIBS} ${Boost_LIBRARIES})
endif(UNIX)
target_link_libraries(TestBump PoseExprLib ${DLIB_LIB_DIR}/libdlib.so)
install (TARGETS TestBump DESTINATION .)
