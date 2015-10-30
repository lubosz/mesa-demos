include_directories(
	${CMAKE_SOURCE_DIR}/src/egl/eglut
	${CMAKE_SOURCE_DIR}/src/util
	${EGL_INCLUDE_DIRS}
	${GLESV2_INCLUDE_DIRS}
)

set (subdir egl/opengles2)

set (targets
	es2_info
	es2tri
)

foreach (target ${targets})
  if (X11_FOUND)
		add_executable (${target} ${target}.c)
		target_link_libraries (${target} ${EGL_LIBRARIES} ${GLESV2_LIBRARIES} ${X11_X11_LIB})
		install (TARGETS ${target} DESTINATION ${subdir})
  endif ()
endforeach (target)


# Targets that can be built both for fullscreen EGL and X11

set (targets
	es2gears
)

foreach (target ${targets})
	if (X11_FOUND)
		add_executable (${target}_x11 ${target}.c)
		target_link_libraries (${target}_x11 eglut_x11 ${GLESV2_LIBRARIES})
		install (TARGETS ${target}_x11 DESTINATION ${subdir})
	endif ()
	if (WAYLAND_FOUND)
		add_executable (${target}_wayland ${target}.c)
		target_link_libraries (${target}_wayland eglut_wayland ${GLESV2_LIBRARIES})
		install (TARGETS ${target}_wayland DESTINATION ${subdir})
	endif ()
endforeach (target)
