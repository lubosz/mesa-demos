include_directories (
	${EGL_INCLUDE_DIRS}
)

if (X11_FOUND)
	add_library (eglut_x11 eglut.h eglut.c eglutint.h eglut_x11.c)
	target_link_libraries (eglut_x11 ${EGL_LIBRARIES} ${X11_X11_LIB})
	if (BUILD_SHARED_LIBS)
		install (TARGETS eglut_x11 DESTINATION ${LIBDIR})
	endif (BUILD_SHARED_LIBS)
endif (X11_FOUND)

if(WAYLAND_FOUND)
	add_library (eglut_wayland eglut.h eglut.c eglutint.h eglut_wayland.c)
	target_link_libraries (eglut_wayland ${EGL_LIBRARIES} ${WAYLAND_LIBRARIES} ${WAYLAND_EGL_LIBRARIES})
	if (BUILD_SHARED_LIBS)
		install (TARGETS eglut_wayland DESTINATION ${LIBDIR})
	endif (BUILD_SHARED_LIBS)
endif(WAYLAND_FOUND)

