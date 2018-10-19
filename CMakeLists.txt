cmake_minimum_required(VERSION 2.8.3)
project (vcglib)

add_definitions (-std=c++11)

find_package (Eigen3 REQUIRED NO_MODULE)

include_directories (${CMAKE_CURRENT_SOURCE_DIR}
	${EIGEN3_INCLUDE_DIRS}
)
add_library(plylib SHARED
	wrap/ply/plylib.cpp
)
target_link_libraries(plylib)

set(CMAKE_INSTALL_PREFIX /usr/local)
message("Installing in directory = ${CMAKE_INSTALL_PREFIX}")

install(TARGETS plylib
	LIBRARY DESTINATION ${CMAKE_INSTALL_PREFIX}/lib
)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/wrap
	DESTINATION ${CMAKE_INSTALL_PREFIX}/include
	FILES_MATCHING PATTERN "*.h"
)
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/vcg
	DESTINATION ${CMAKE_INSTALL_PREFIX}/include
	FILES_MATCHING PATTERN "*.h"
)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/apps/metro
	DESTINATION ${CMAKE_INSTALL_PREFIX}/include
	FILES_MATCHING PATTERN "*.h"
)
