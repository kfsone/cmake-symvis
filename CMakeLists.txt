# main <- liba
#  liba -> libb
#   libb -> libc	[defines first 'terminal']
#   libb -> libd
#    libd -> libe	[defines second 'terminal']

cmake_minimum_required (VERSION 3.20)
project (visibility LANGUAGES CXX)
set (CMAKE_CXX_STANDARD 17)
set (CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable (main main.cpp)
target_link_libraries (main PUBLIC liba)

add_subdirectory (liba)
add_subdirectory (libb)
add_subdirectory (libc)
add_subdirectory (libd)
add_subdirectory (libe)

