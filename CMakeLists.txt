cmake_minimum_required(VERSION 3.5.0)

# This is JK2MV superproject
project("JK2MV" HOMEPAGE_URL "https://jk2mv.org" LANGUAGES C CXX)

include(ExternalProject)

ExternalProject_Add(libjpeg-turbo
  GIT_REPOSITORY https://github.com/libjpeg-turbo/libjpeg-turbo.git
  GIT_TAG 3.0.3
  GIT_SHALLOW TRUE
  BUILD_COMMAND ${CMAKE_COMMAND} --build . --target jpeg-static
  CMAKE_ARGS
  -DCMAKE_INSTALL_PREFIX=<INSTALL_DIR>
  -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
  -DENABLE_SHARED=0
  -DWITH_ARITH_DEC=0
  -DWITH_ARITH_ENC=0
  -DWITH_TURBOJPEG=0
)

ExternalProject_Get_Property(libjpeg-turbo INSTALL_DIR)
ExternalProject_Add(jk2mv-engine
  SOURCE_DIR "${CMAKE_SOURCE_DIR}/src"
  DEPENDS libjpeg-turbo
  CMAKE_ARGS
  -DCMAKE_INSTALL_PREFIX=<INSTALL_DIR>
  -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
  -DLIBJPEG_TURBO_PACKAGE_PATH=${INSTALL_DIR}
)
