cmake_minimum_required(VERSION 3.10)

project(microtar VERSION 1.0)

add_library(microtar OBJECT src/microtar.c)
set_property(TARGET microtar PROPERTY POSITION_INDEPENDENT_CODE 1)
target_include_directories(microtar PUBLIC "src")
set_target_properties(microtar PROPERTIES PUBLIC_HEADER src/microtar.h)

add_library(microtar_shared SHARED $<TARGET_OBJECTS:microtar>)
set_target_properties(microtar_shared PROPERTIES OUTPUT_NAME microtar)

add_library(microtar_static STATIC $<TARGET_OBJECTS:microtar>)
set_target_properties(microtar_static PROPERTIES OUTPUT_NAME microtar)

add_compile_options(-Wall)

install(TARGETS microtar_shared microtar_static
	LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
	PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
