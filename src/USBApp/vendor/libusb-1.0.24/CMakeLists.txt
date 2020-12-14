# CMakeList.txt : CMake project for USBApp, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

set(project_name "libusb")
project(${project_name})

include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}
	${CMAKE_CURRENT_SOURCE_DIR}/msvc
	${CMAKE_CURRENT_SOURCE_DIR}/libusb
)
link_directories(
	${CMAKE_CURRENT_BINARY_DIR}
)

if(MSVC)
	file(GLOB LIBUSB_SRCS 
		"${CMAKE_CURRENT_SOURCE_DIR}/libusb/core.c"
		"${CMAKE_CURRENT_SOURCE_DIR}/libusb/descriptor.c"
		"${CMAKE_CURRENT_SOURCE_DIR}/libusb/os/events_windows.c"
		"${CMAKE_CURRENT_SOURCE_DIR}/libusb/hotplug.c"
		"${CMAKE_CURRENT_SOURCE_DIR}/libusb/io.c"
		"${CMAKE_CURRENT_SOURCE_DIR}/libusb/sync.c"
		"${CMAKE_CURRENT_SOURCE_DIR}/libusb/strerror.c"
		"${CMAKE_CURRENT_SOURCE_DIR}/libusb/os/threads_windows.c"
		"${CMAKE_CURRENT_SOURCE_DIR}/libusb/os/windows_common.c"
		"${CMAKE_CURRENT_SOURCE_DIR}/libusb/os/windows_usbdk.c"
		"${CMAKE_CURRENT_SOURCE_DIR}/libusb/os/windows_winusb.c"
	)
	set(EXT_LIB setupapi comctl32 shlwapi)
else(MSVC)
endif(MSVC)
# Add source to this project's executable.
add_library (${project_name} STATIC ${LIBUSB_SRCS})

target_compile_options(${project_name} PRIVATE "/utf-8")
target_link_libraries(${project_name} 
	PRIVATE ${EXT_LIB}
)

if(MSVC)
	file(GLOB EXAMPLES_LISTDEVS_SRCS 
		"${CMAKE_CURRENT_SOURCE_DIR}/examples/listdevs.c"
	)
	set(EXT_LIB setupapi comctl32 shlwapi)
else(MSVC)
endif(MSVC)
add_executable(${project_name}_examples_listdevs ${EXAMPLES_LISTDEVS_SRCS})

target_link_libraries(${project_name}_examples_listdevs
	PRIVATE ${project_name}
)
# TODO: Add tests and install targets if needed.
