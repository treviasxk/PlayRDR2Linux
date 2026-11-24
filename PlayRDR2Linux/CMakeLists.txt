cmake_minimum_required(VERSION 3.16)

project(PlayRDR2Linux)

add_link_options(${LINK_OPTIONS})
add_executable(PlayRDR2Linux ${CMAKE_SOURCE_DIR}/main.c)

target_link_libraries(PlayRDR2Linux ${WIN_LIBRARIES})
