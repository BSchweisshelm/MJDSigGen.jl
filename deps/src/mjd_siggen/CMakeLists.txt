# Actually requires cmake v2.8.12 on OS-X for CMAKE_MACOSX_RPATH, but
# Travis CI only offers 2.8.7 on Linux
cmake_minimum_required (VERSION 2.8.7)

project (mjd_siggen)

set (CMAKE_BUILD_TYPE Release)

set (CMAKE_MACOSX_RPATH ON)
set (CMAKE_SKIP_BUILD_RPATH FALSE)
set (CMAKE_BUILD_WITH_INSTALL_RPATH FALSE)
set (CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")
set (CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

# include_directories (${CMAKE_CURRENT_SOURCE_DIR})

add_library (mjd_siggen SHARED calc_signal.c cyl_point.c detector_geometry.c fields.c point.c read_config.c)

add_executable (mjd_fieldgen mjd_fieldgen.c)
target_link_libraries (mjd_fieldgen LINK_PUBLIC mjd_siggen)

target_link_libraries (mjd_siggen -lm)

install (TARGETS mjd_siggen DESTINATION lib)
install (TARGETS mjd_fieldgen DESTINATION bin)
install (FILES calc_signal.h cyl_point.h detector_geometry.h fields.h mjd_siggen.h point.h DESTINATION include)
