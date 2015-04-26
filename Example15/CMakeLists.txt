PROJECT(Example15)

CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/../Binaries/)
set(CMAKE_BUILD_TYPE Release)

find_package( OpenGL REQUIRED )
find_package( GLUT REQUIRED )
find_library( OIIO "OpenImageIO" "/usr/local/lib")
find_library( GLUS "GLUS" "/Users/Xin/openglex/GLUS/build")
find_library( GLEW "GLEW" "/usr/local/lib")
find_library( GLFW3 "GLFW3" "/usr/local/lib")

MESSAGE ( STATUS "OIIO found: " ${OIIO})
MESSAGE ( STATUS "GLUS found: " ${GLUS})
MESSAGE ( STATUS "GLFW3 found: " ${GLFW3})
MESSAGE ( STATUS "GLEW found: " ${GLEW})

FILE(GLOB header ${CMAKE_CURRENT_SOURCE_DIR}/src/*.c)

include_directories("/usr/local/include" ${OPENGL_INCLUDE_DIR} ${GLUT_INCLUDE_DIR} "/Users/Xin/openglex/GLUS/src")


set(SOURCE_FILES ${header} src/main.c)
add_executable(ex15 ${SOURCE_FILES})
TARGET_LINK_LIBRARIES(ex15 ${GLUT_LIBRARIES} ${OPENGL_LIBRARIES} ${OIIO} ${GLUS} ${GLEW} ${GLFW3})