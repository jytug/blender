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
# ***** END GPL LICENSE BLOCK *****

set(INC
	.
)

set(INC_SYS

)

set(SRC
	utfconv.c

	utfconv.h
)

# This is odd but leave it for now...
# Why have win32 check here? - this is only used for windows.
# ... because one day we might want to use it on other platforms.
if(WIN32)
	list(APPEND SRC
		utf_winfunc.c
		utf_winfunc.h
	)
endif()

blender_add_lib(bf_intern_utfconv "${SRC}" "${INC}" "${INC_SYS}")
