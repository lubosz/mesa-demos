include_directories(
	${CMAKE_SOURCE_DIR}/src/egl/eglut
	${CMAKE_SOURCE_DIR}/src/util
	${EGL_INCLUDE_DIRS}
	${OPENGL_INCLUDE_PATH}
)

link_libraries (
	${EGL_LIBRARIES}
	${OPENGL_gl_LIBRARY}
)

set (subdir egl)

# Targets that can be built both for fullscreen EGL and X11

set (targets
	egltri
	eglgears
)

foreach (target ${targets})
	if (X11_FOUND)
		add_executable (${target}_x11 ${target}.c)
		target_link_libraries (${target}_x11 eglut_x11)
		install (TARGETS ${target}_x11 DESTINATION ${subdir})
	endif ()
endforeach (target)


if (X11_FOUND)
	add_executable (xeglgears xeglgears.c)
	target_link_libraries (xeglgears ${X11_X11_LIB})

	add_executable (xeglthreads xeglthreads.c)
	target_link_libraries (xeglthreads ${X11_X11_LIB})
endif (X11_FOUND)

