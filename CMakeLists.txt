cmake_minimum_required (VERSION 2.6)
project (psexample)
# The version number.
set (psexample_VERSION_MAJOR 1)
set (psexample_VERSION_MINOR 0)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/bin")
set(PROJECT_SOURCE_DIR "${PROJECT_SOURCE_DIR}/src")

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake/Modules")
find_package(PkgConfig 0.2 REQUIRED)

find_package(SphinxBase REQUIRED)
find_package(PocketSphinx REQUIRED )

configure_file (
  "${PROJECT_SOURCE_DIR}/include/PSExample.h.in"
  "${PROJECT_BINARY_DIR}/include/PSExample.h"
  )
 
# add the binary tree to the search path for include files
# so that we will find TutorialConfig.h
include_directories("${PROJECT_BINARY_DIR}/include")
include_directories (${POCKETSPHINX_INCLUDE_DIRS})

# add the executable
add_executable(psexample "${PROJECT_SOURCE_DIR}/hello_ps.c")
target_link_libraries( psexample ${POCKETSPHINX_LIBRARIES} ${SPHINXBASE_LIBRARIES} )
file (COPY "${PROJECT_SOURCE_DIR}/goforward.raw" DESTINATION ${CMAKE_RUNTIME_OUTPUT_DIRECTORY})
 
