cmake_policy(SET CMP0021 OLD)

set(INC
	..
)

set(SRC
	node.cpp
	node_type.cpp
	node_xml.cpp
)

set(SRC_HEADERS
	node.h
	node_enum.h
	node_type.h
	node_xml.h
)

include_directories(${INC})
include_directories(SYSTEM ${INC_SYS})

add_library(cycles_graph ${SRC} ${SRC_HEADERS})

