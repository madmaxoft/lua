# Simple CMakeLists.txt for building Lua as a static library
cmake_minimum_required(VERSION 2.4.4)
project (lua CXX)

if(MSVC)
    # set(CMAKE_DEBUG_POSTFIX "d")
    add_definitions(-D_CRT_SECURE_NO_DEPRECATE)
    add_definitions(-D_CRT_NONSTDC_NO_DEPRECATE)
    include_directories(${CMAKE_CURRENT_SOURCE_DIR})
endif()

set (LUA_SRCS
	lapi.c
	lauxlib.c
	lbaselib.c
	lbitlib.c
	lcode.c
	lcorolib.c
	lctype.c
	ldblib.c
	ldebug.c
	ldo.c
	ldump.c
	lfunc.c
	lgc.c
	linit.c
	liolib.c
	llex.c
	lmathlib.c
	lmem.c
	loadlib.c
	lobject.c
	lopcodes.c
	loslib.c
	lparser.c
	lstate.c
	lstring.c
	lstrlib.c
	ltable.c
	ltablib.c
	ltests.c
	ltm.c
	lua.c
	lundump.c
	lutf8lib.c
	lvm.c
	lzio.c
)

set (LUA_HDRS
	lapi.h
	lauxlib.h
	lcode.h
	lctype.h
	ldebug.h
	ldo.h
	lfunc.h
	lgc.h
	llex.h
	llimits.h
	lmem.h
	lobject.h
	lopcodes.h
	lparser.h
	lprefix.h
	lstate.h
	lstring.h
	ltable.h
	ltests.h
	ltm.h
	lua.h
	luaconf.h
	lualib.h
	lundump.h
	lvm.h
	lzio.h
)

# TODO: We need this to handle Lua errors as exceptions, but it breaks static libraries' ABI
# set_source_files_properties(${LUA_SRCS} PROPERTIES LANGUAGE CXX)

add_library(lua STATIC
	${LUA_SRCS}
	${LUA_HDRS}
)

target_include_directories(lua
	SYSTEM INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
)
