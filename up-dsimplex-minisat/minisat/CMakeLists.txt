include_directories(mtl)
file(GLOB srcs core/*.C)
add_executable(up-dsimplex-minisat ${srcs})
target_link_libraries(up-dsimplex-minisat z matrix)
install(TARGETS up-dsimplex-minisat ${INSTALL_OPTS})
