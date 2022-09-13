cmake_policy(SET CMP0021 OLD)

# Python CTests
if(WITH_BLENDER)
	add_subdirectory(python)
endif()

# GTest
add_subdirectory(gtests)
