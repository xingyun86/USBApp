# CMakeList.txt : CMake project for USBApp, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

set(project_name "USBApp")
project(${project_name})

include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}
)
link_directories(
	${CMAKE_CURRENT_BINARY_DIR}
)
file(GLOB SRCS "*.cpp" "*.c" "*.rc")
if(MSVC)
set(EXT_LIB setupapi comctl32 shlwapi)
else(MSVC)
endif(MSVC)
# Add source to this project's executable.
add_executable (${project_name} ${SRCS})

target_link_libraries(${project_name} 
	PRIVATE ${EXT_LIB}
)
# TODO: Add tests and install targets if needed.
