PROJECT(Examples)

CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/Binaries/)
set(CMAKE_BUILD_TYPE Release)

set(GLUS_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/GLUS")
find_package( OpenGL REQUIRED )
find_package( GLUT REQUIRED )
find_library( GLUS "GLUS" ${GLUS_DIRECTORY}/lib)
find_library( GLEW "GLEW" "/usr/local/lib")
find_library( GLFW3 "GLFW3" "/usr/local/lib")
include_directories("/usr/local/include" ${OPENGL_INCLUDE_DIR} ${GLUT_INCLUDE_DIR} ${GLUS_DIRECTORY}/src)

MESSAGE ( STATUS "GLUS found: " ${GLUS})
MESSAGE ( STATUS "GLFW3 found: " ${GLFW3})
MESSAGE ( STATUS "GLEW found: " ${GLEW})

foreach(_var RANGE 01 44)
SET (NameString "Example${_var}")
STRING(LENGTH "${NameString}" length)
if (${length} LESS  9)
SET (NameString "Example0${_var}")
endif()
MESSAGE(${NameString})

FILE(GLOB SOURCE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/${NameString}/src/*.c)
add_executable("${NameString}" ${SOURCE_FILES})
TARGET_LINK_LIBRARIES("${NameString}" ${GLUT_LIBRARIES} ${OPENGL_LIBRARIES} ${GLUS} ${GLEW} ${GLFW3})

endforeach()

