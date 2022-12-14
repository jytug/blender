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
# The Original Code is Copyright (C) 2016, Blender Foundation
# All rights reserved.
#
# Contributor(s): Blender Foundation,
#                 Sergey Sharybin
#
# ***** END GPL LICENSE BLOCK *****

set(INC
	src
	../gflags/src
)

set(INC_SYS
)

set(SRC
	src/logging.cc
	src/raw_logging.cc
	src/utilities.cc
	src/vlog_is_on.cc

	src/utilities.h

	src/config.h
	src/config_freebsd.h
	src/config_hurd.h
	src/config_linux.h
	src/config_mac.h

	src/base/commandlineflags.h
	src/base/googleinit.h
	src/base/mutex.h

	src/stacktrace.h
	src/stacktrace_generic-inl.h
	src/stacktrace_libunwind-inl.h
	src/stacktrace_powerpc-inl.h
	src/stacktrace_x86_64-inl.h
	src/stacktrace_x86-inl.h
)

if(WIN32)
	list(APPEND SRC
		src/windows/port.cc

		src/windows/glog/raw_logging.h
		src/windows/glog/vlog_is_on.h
		src/windows/glog/logging.h
		src/windows/glog/log_severity.h
		src/windows/port.h
		src/windows/config.h
	)

	list(APPEND INC
		src/windows
	)
else()
	list(APPEND SRC
		src/demangle.cc
		src/signalhandler.cc
		src/symbolize.cc

		src/demangle.h
		src/glog/logging.h
		src/glog/log_severity.h
		src/glog/raw_logging.h
		src/glog/vlog_is_on.h
		src/symbolize.h
	)
endif()

add_definitions(${GFLAGS_DEFINES})
add_definitions(${GLOG_DEFINES})

blender_add_lib(extern_glog "${SRC}" "${INC}" "${INC_SYS}")
