cmake_minimum_required(VERSION 3.10)

project(microtar VERSION 1.0)
option(MICROTAR_BUILD_STATIC "Build static microtar" ON)
option(MICROTAR_BUILD_SHARED "Build shared microtar" ON)

add_library(microtar OBJECT src/microtar.c)
set_property(TARGET microtar PROPERTY POSITION_INDEPENDENT_CODE 1)
target_include_directories(microtar PUBLIC "src")
set_target_properties(microtar PROPERTIES PUBLIC_HEADER src/microtar.h)

if(${MICROTAR_BUILD_SHARED})
	add_library(microtar_shared SHARED $<TARGET_OBJECTS:microtar>)
	target_link_libraries(microtar_shared microtar)
	set_target_properties(microtar_shared PROPERTIES OUTPUT_NAME microtar)

	install(TARGETS microtar_shared
		LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
		PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
endif()

if(${MICROTAR_BUILD_STATIC})
	add_library(microtar_static STATIC $<TARGET_OBJECTS:microtar>)
	target_link_libraries(microtar_static microtar)
	set_target_properties(microtar_static PROPERTIES OUTPUT_NAME microtar)

	install(TARGETS microtar_static
		LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
		PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
endif()

add_compile_options(-Wall)
