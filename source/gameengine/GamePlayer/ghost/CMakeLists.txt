cmake_policy(SET CMP0021 OLD)
# ***** BEGIN GPL LICENSE BLOCK *****
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# as published by the Free Software Foundation; either version 2
# of the License, or (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software Foundation,
# Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301, USA.
#
# The Original Code is Copyright (C) 2006, Blender Foundation
# All rights reserved.
#
# The Original Code is: all of this file.
#
# Contributor(s): Jacques Beaurain.
#
# ***** END GPL LICENSE BLOCK *****

set(INC
	.
	../common
	../../BlenderRoutines
	../../Converter
	../../Expressions
	../../GameLogic
	../../Ketsji
	../../Network
	../../Network/LoopBackNetwork
	../../Physics/common
	../../Rasterizer
	../../Rasterizer/RAS_OpenGLRasterizer
	../../SceneGraph
	../../../blender
	../../../blender/blenfont
	../../../blender/blenkernel
	../../../blender/blenlib
	../../../blender/blenloader
	../../../blender/blentranslation
	../../../blender/gpu
	../../../blender/imbuf
	../../../blender/makesdna
	../../../blender/makesrna
	../../../../intern/container
	../../../../intern/ghost
	../../../../intern/glew-mx
	../../../../intern/guardedalloc
	../../../../intern/string
	../../../../intern/memutil
)

set(INC_SYS
	../../../../intern/moto/include
	${GLEW_INCLUDE_PATH}
	${PYTHON_INCLUDE_DIRS}
	${BOOST_INCLUDE_DIR}
)

set(SRC
	GPG_Application.cpp
	GPG_Canvas.cpp
	GPG_KeyboardDevice.cpp
	GPG_System.cpp
	GPG_ghost.cpp

	GPG_Application.h
	GPG_Canvas.h
	GPG_KeyboardDevice.h
	GPG_System.h
)

add_definitions(${GL_DEFINITIONS})

if(WIN32)
	blender_include_dirs(../../../../intern/utfconv)
endif()

if(WITH_INPUT_NDOF)
	add_definitions(-DWITH_INPUT_NDOF)
endif(WITH_INPUT_NDOF)

if(WITH_CODEC_FFMPEG)
	add_definitions(-DWITH_FFMPEG)
endif()

if(WITH_INTERNATIONAL)
	add_definitions(-DWITH_INTERNATIONAL)
endif()

if(WITH_AUDASPACE)
	add_definitions(${AUDASPACE_DEFINITIONS})

	list(APPEND INC_SYS
		${AUDASPACE_C_INCLUDE_DIRS}
	)
endif()

if(WITH_SDL AND WITH_SDL_DYNLOAD)
	list(APPEND INC
		../../../../extern/sdlew/include
	)
	add_definitions(-DWITH_SDL_DYNLOAD)
endif()

blender_add_lib_nolist(ge_player_ghost "${SRC}" "${INC}" "${INC_SYS}")
