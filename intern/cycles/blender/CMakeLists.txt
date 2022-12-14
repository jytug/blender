cmake_policy(SET CMP0021 OLD)

set(INC
	..
	../../glew-mx
	../../guardedalloc
	../../mikktspace
	../../../source/blender/makesdna
	../../../source/blender/makesrna
	../../../source/blender/blenlib
	${CMAKE_BINARY_DIR}/source/blender/makesrna/intern
)

set(INC_SYS
	${PYTHON_INCLUDE_DIRS}
	${GLEW_INCLUDE_DIR}
)

set(SRC
	blender_camera.cpp
	blender_mesh.cpp
	blender_object.cpp
	blender_object_cull.cpp
	blender_particles.cpp
	blender_curves.cpp
	blender_logging.cpp
	blender_python.cpp
	blender_session.cpp
	blender_shader.cpp
	blender_sync.cpp
	blender_texture.cpp

	CCL_api.h
	blender_object_cull.h
	blender_sync.h
	blender_session.h
	blender_texture.h
	blender_util.h
)

set(ADDON_FILES
	addon/__init__.py
	addon/engine.py 
	addon/osl.py
	addon/presets.py
	addon/properties.py
	addon/ui.py
	addon/version_update.py
)

add_definitions(${GL_DEFINITIONS})

if(WITH_CYCLES_NETWORK)
	add_definitions(-DWITH_NETWORK)
endif()

blender_add_lib(bf_intern_cycles "${SRC}" "${INC}" "${INC_SYS}")

# avoid link failure with clang 3.4 debug
if(CMAKE_C_COMPILER_ID MATCHES "Clang" AND NOT ${CMAKE_C_COMPILER_VERSION} VERSION_LESS '3.4')
	set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -gline-tables-only")
endif()

add_dependencies(bf_intern_cycles bf_rna)

delayed_install(${CMAKE_CURRENT_SOURCE_DIR} "${ADDON_FILES}" ${CYCLES_INSTALL_PATH})

