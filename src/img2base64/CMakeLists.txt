set (libname "img2base64")
set (libdescription "upm for img2base64")
set (module_src ${libname}.cxx ${CMAKE_CURRENT_SOURCE_DIR}/lib/libb64/src/cencode.c)
set (module_h ${libname}.h)
FIND_PACKAGE(OpenCV REQUIRED)
INCLUDE_DIRECTORIES(${OpenCV_INCLUDE_DIR})
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/lib/libb64/include)
upm_module_init()
target_link_libraries(${libname} ${OpenCV_LIBS} pthread)
if (BUILDSWIG)
	if (BUILDSWIGNODE)
		swig_link_libraries (jsupm_${libname} ${OpenCV_LIBS} pthread ${NODE_LIBRARIES})
	endif()
	if (BUILDSWIGPYTHON)
		swig_link_libraries (pyupm_${libname} ${OpenCV_LIBS} pthread ${PYTHON_LIBRARIES})
	endif()
endif()
