cmake_minimum_required(VERSION 3.10)

project(microtar VERSION 1.0)

add_library(microtar src/microtar.h src/microtar.c)
target_include_directories(microtar PUBLIC "src")
set_target_properties(microtar PROPERTIES PUBLIC_HEADER src/microtar.h)

add_compile_options(-Wall)