#top dir cmake project for libairspyhf

cmake_minimum_required(VERSION 2.8)
project (airspyhf_all)

#provide missing strtoull() for VC11
if(MSVC11)
    add_definitions(-Dstrtoull=_strtoui64)
endif(MSVC11)

add_subdirectory(libairspyhf)