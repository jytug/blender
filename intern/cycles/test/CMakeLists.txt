cmake_policy(SET CMP0021 OLD)
if(WITH_GTESTS)
	Include(GTestTesting)

	# Otherwise we get warnings here that we cant fix in external projects
	remove_strict_flags()
endif()

macro(CYCLES_TEST SRC EXTRA_LIBS)
	if(WITH_GTESTS)
		BLENDER_SRC_GTEST("cycles_${SRC}" "${SRC}_test.cpp" "${EXTRA_LIBS}")
	endif()
endmacro()

set(INC
	.
	..
	../device
	../graph
	../kernel
	../render
	../util
)

set(ALL_CYCLES_LIBRARIES
	cycles_render
	cycles_device
	cycles_bvh
	cycles_graph
	cycles_subd
	cycles_util
	${OPENIMAGEIO_LIBRARIES}
)
if(WITH_CYCLES_OSL)
	list(APPEND ALL_CYCLES_LIBRARIES
		cycles_kernel_osl
		${OSL_LIBRARIES}
		${LLVM_LIBRARIES}
	)
endif()
if(WITH_IMAGE_OPENJPEG AND NOT WITH_SYSTEM_OPENJPEG)
	list(APPEND ALL_CYCLES_LIBRARIES
		extern_openjpeg
	)
endif()
if(WITH_CYCLES_OPENSUBDIV)
	add_definitions(-DWITH_OPENSUBDIV)
	include_directories(
		SYSTEM
		${OPENSUBDIV_INCLUDE_DIR}
	)
	list(APPEND ALL_CYCLES_LIBRARIES
		${OPENSUBDIV_LIBRARIES}
	)
endif()
list(APPEND ALL_CYCLES_LIBRARIES
	${BOOST_LIBRARIES}
	${PNG_LIBRARIES}
	${JPEG_LIBRARIES}
	${ZLIB_LIBRARIES}
	${TIFF_LIBRARY}
	${OPENIMAGEIO_LIBRARIES}
	${OPENEXR_LIBRARIES}
)

include_directories(${INC})

link_directories(${OPENIMAGEIO_LIBPATH}
                 ${BOOST_LIBPATH}
                 ${PNG_LIBPATH}
                 ${JPEG_LIBPATH}
                 ${ZLIB_LIBPATH}
                 ${TIFF_LIBPATH}
                 ${OPENEXR_LIBPATH})

set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${PLATFORM_LINKFLAGS}")
set(CMAKE_EXE_LINKER_FLAGS_DEBUG "${CMAKE_EXE_LINKER_FLAGS_DEBUG} ${PLATFORM_LINKFLAGS_DEBUG}")

CYCLES_TEST(render_graph_finalize "${ALL_CYCLES_LIBRARIES}")
CYCLES_TEST(util_aligned_malloc "cycles_util")
CYCLES_TEST(util_path "cycles_util;${BOOST_LIBRARIES};${OPENIMAGEIO_LIBRARIES}")
CYCLES_TEST(util_string "cycles_util;${BOOST_LIBRARIES}")
CYCLES_TEST(util_task "cycles_util;${BOOST_LIBRARIES}")
