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
# The Original Code is Copyright (C) 2011 Blender Foundation.
#
# Contributor(s): Blender Foundation,
#                 Sergey Sharybin
#
# ***** END GPL LICENSE BLOCK *****

set(INC
	../include
	../../blenfont
	../../blenkernel
	../../blenlib
	../../blentranslation
	../../imbuf
	../../gpu
	../../makesdna
	../../makesrna
	../../windowmanager
	../../../../intern/guardedalloc
	../../../../intern/glew-mx
)

set(INC_SYS
	${GLEW_INCLUDE_PATH}
)

set(SRC
	clip_buttons.c
	clip_dopesheet_draw.c
	clip_dopesheet_ops.c
	clip_draw.c
	clip_editor.c
	clip_graph_draw.c
	clip_graph_ops.c
	clip_ops.c
	clip_toolbar.c
	clip_utils.c
	space_clip.c
	tracking_ops.c
	tracking_ops_detect.c
	tracking_ops_orient.c
	tracking_ops_plane.c
	tracking_ops_solve.c
	tracking_ops_track.c
	tracking_ops_stabilize.c
	tracking_ops_utils.c
	tracking_select.c

	clip_intern.h
	tracking_ops_intern.h
)

add_definitions(${GL_DEFINITIONS})

if(WITH_INTERNATIONAL)
	add_definitions(-DWITH_INTERNATIONAL)
endif()

blender_add_lib(bf_editor_space_clip "${SRC}" "${INC}" "${INC_SYS}")
