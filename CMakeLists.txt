cmake_minimum_required(VERSION 3.14)
project(sdl2_gfx C)

set(CMAKE_C_STANDARD 11)
set(PROJECT_NAME SDL2_gfx)


list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

set(CMAKE_THREAD_LIBS_INIT "-lpthread")
set(CMAKE_HAVE_THREADS_LIBRARY 1)
set(CMAKE_USE_WIN32_THREADS_INIT 0)
set(CMAKE_USE_PTHREADS_INIT 1)
set(THREADS_PREFER_PTHREAD_FLAG ON)

include_directories(src)

set(SOURCE src/SDL2_framerate.c
        src/SDL2_gfxPrimitives.c
        src/SDL2_imageFilter.c
        src/SDL2_rotozoom.c)

set(HEADERS src/SDL2_framerate.h
        src/SDL2_gfxPrimitives.h
        src/SDL2_gfxPrimitives_font.h
        src/SDL2_imageFilter.h
        src/SDL2_rotozoom.h)

set(CMAKE_BINARY_DIR ${CMAKE_CURRENT_SOURCE_DIR}/build/bin)

add_library(${PROJECT_NAME} SHARED ${SOURCE} ${HEADERS})

add_library(${PROJECT_NAME}.lib STATIC ${SOURCE} ${HEADERS})

file(COPY ${HEADERS}
        DESTINATION ${CMAKE_CURRENT_SOURCE_DIR}/build/include)


set(SDL2_PATH "C:\\SDL2")

find_package(SDL2 REQUIRED)

target_link_libraries(${PROJECT_NAME} SDL2::Main)
target_link_libraries(${PROJECT_NAME}.lib SDL2::Main)