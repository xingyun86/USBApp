# CMakeList.txt : Top-level CMake project file, do global configuration
# and include sub-projects here.
#
cmake_minimum_required (VERSION 3.8)

project ("USBApp")

if(MSVC)
add_compile_definitions(
	_CRT_SECURE_NO_WARNINGS
)
else(MSVC)
endif(MSVC)

# Include sub-projects.
add_subdirectory ("USBApp")
