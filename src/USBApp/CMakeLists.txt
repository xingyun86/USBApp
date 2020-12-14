# CMakeList.txt : Top-level CMake project file, do global configuration
# and include sub-projects here.
#
cmake_minimum_required (VERSION 3.8)

project ("USBApp")

if(MSVC)
	set(ADMIN_LEVEL "/MANIFESTUAC:\"level='requireAdministrator' uiAccess='false'\"")
	add_compile_definitions(
		_CRT_SECURE_NO_WARNINGS
		_WINSOCK_DEPRECATED_NO_WARNINGS
		_WIN32_WINNT=_WIN32_WINNT_WINXP
		#_WIN32_WINNT=_WIN32_WINNT_VISTA
	)

	MESSAGE(STATUS "CMAKE_BUILD_TYPE=" ${CMAKE_BUILD_TYPE})

	set(CompilerFlags
		CMAKE_CXX_FLAGS
		CMAKE_CXX_FLAGS_DEBUG
		CMAKE_CXX_FLAGS_RELEASE
		CMAKE_C_FLAGS
		CMAKE_C_FLAGS_DEBUG
		CMAKE_C_FLAGS_RELEASE
		)
	foreach(CompilerFlag ${CompilerFlags})
		string(REPLACE "/MD" "/MT" ${CompilerFlag} "${${CompilerFlag}}")
	endforeach()
else(MSVC)
endif(MSVC)

# Include sub-projects.
add_subdirectory ("vendor/libusb-1.0.24")
add_subdirectory ("USBApp")
add_subdirectory ("LibUsbApp")
