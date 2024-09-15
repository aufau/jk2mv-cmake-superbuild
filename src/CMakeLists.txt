cmake_minimum_required(VERSION 3.5.0)

# This is JK2MV superproject
project("jk2mv-engine" HOMEPAGE_URL "https://jk2mv.org" LANGUAGES C)

set(CMAKE_C_STANDARD 99)

set(LIBJPEG_TURBO_PACKAGE_PATH "" CACHE PATH "Path where libjpeg-turbo CMake config can be found")
mark_as_advanced(LIBJPEG_TURBO_PACKAGE_PATH)

find_package(libjpeg-turbo REQUIRED PATHS "${LIBJPEG_TURBO_PACKAGE_PATH}" NO_DEFAULT_PATH)

add_executable(jk2mv jk2mv.c)
target_link_libraries(jk2mv PUBLIC libjpeg-turbo::jpeg-static)

install(TARGETS jk2mv DESTINATION bin)
