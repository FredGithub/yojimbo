cmake_minimum_required(VERSION 3.0)
project(yojimbo VERSION "1.0")

# includes
include_directories(
	netcode.io
	reliable.io
)

if(MSVC)
	include_directories(windows)
elseif(ANDROID)
	include_directories(android/sodium/include)
	include_directories(android/mbedtls/include)
elseif(EMSCRIPTEN)
	include_directories(emscripten/sodium/include)
	include_directories(emscripten/mbedtls/include)
endif()

# sources
file(GLOB_RECURSE PROJECT_SOURCES
	yojimbo.h
	yojimbo.cpp
	tlsf/tlsf.h
	tlsf/tlsf.c
	netcode.io/netcode.c
	netcode.io/netcode.h
	reliable.io/reliable.c
	reliable.io/reliable.h
)

add_library(${PROJECT_NAME} ${PROJECT_SOURCES})
