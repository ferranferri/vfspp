cmake_minimum_required(VERSION 3.17)
project(vfspp
        VERSION 0.0.1.0
        DESCRIPTION "VFSPP"
        HOMEPAGE_URL TBD
        LANGUAGES C CXX)

# global definitions for the project
set(CMAKE_CXX_STANDARD 17)

SET(PLATFORM "macOS")
if (${PLATFORM} STREQUAL "macOS" OR
        ${PLATFORM} STREQUAL "iOS" OR
        ${PLATFORM} STREQUAL "tvOS" OR
        ${PLATFORM} STREQUAL "watchOS")
    set(CMAKE_MACOSX_RPATH 1)
endif()
Include(FetchContent)
FetchContent_Declare(
        ZLIB
        GIT_REPOSITORY git@github.com:madler/zlib.git
        GIT_TAG         v1.2.11)

FetchContent_MakeAvailable(ZLIB)
find_package(ZLIB)
add_library(vfspp STATIC
        include/CFileInfo.h
        include/CMemoryFile.h
        include/CMemoryFileSystem.h
        include/CNativeFile.h
        include/CNativeFileSystem.h
        include/CVirtualFileSystem.h
        include/CZipFile.h
        include/CZipFileSystem.h
        include/IFile.h
        include/IFileSystem.h
        include/VFS.h
        src/CFileInfo.cpp
        src/CMemoryFile.cpp
        src/CMemoryFileSystem.cpp
        src/CNativeFile.cpp
        src/CNativeFileSystem.cpp
        src/CStringUtilsVFS.cpp
        src/CStringUtilsVFS.h
        src/CVirtualFileSystem.cpp
        src/CZipFile.cpp
        src/CZipFileSystem.cpp
        src/miniz.c
        src/miniz.h
        )

target_link_libraries(vfspp ZLIB::ZLIB)
target_include_directories(vfspp PUBLIC include)


add_executable(vfspp_sample examples/example.cpp)
target_link_libraries(vfspp_sample PUBLIC vfspp)
target_include_directories(vfspp_sample PUBLIC include)