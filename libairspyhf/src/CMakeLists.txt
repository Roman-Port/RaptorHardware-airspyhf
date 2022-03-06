#
# Copyright (c) 2012, Jared Boone <jared@sharebrained.com>
# Copyright (c) 2013, Michael Ossmann <mike@ossmann.com>
# Copyright (c) 2013, Youssef Touil <youssef@airspy.com>
# Copyright (c) 2013/2014, Benjamin Vernoux <bvernoux@airspy.com>
#
# This file is part of AirSpy HF+ (based on HackRF project).
#
# All rights reserved.
#
# Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:
#
#     Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
#     Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the
# 	documentation and/or other materials provided with the distribution.
#     Neither the name of Great Scott Gadgets nor the names of its contributors may be used to endorse or promote products derived from this software
# 	without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
# THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED.
# IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
# (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
# ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
#
# Based heavily upon the libftdi cmake setup.

macro(use_c99)
  if (CMAKE_VERSION VERSION_LESS "3.1")
    if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
      set (CMAKE_C_FLAGS "-std=gnu99 ${CMAKE_C_FLAGS}")
    endif ()
  else ()
    set (CMAKE_C_STANDARD 99)
  endif ()
endmacro(use_c99)

use_c99()

# Targets
set(c_sources ${CMAKE_CURRENT_SOURCE_DIR}/airspyhf.c ${CMAKE_CURRENT_SOURCE_DIR}/iqbalancer.c CACHE INTERNAL "List of C sources")
set(c_headers ${CMAKE_CURRENT_SOURCE_DIR}/airspyhf.h ${CMAKE_CURRENT_SOURCE_DIR}/iqbalancer.h ${CMAKE_CURRENT_SOURCE_DIR}/airspyhf_commands.h CACHE INTERNAL "List of C headers")

# Static library
add_library(airspyhf-static STATIC ${c_sources})
set_target_properties(airspyhf-static PROPERTIES CLEAN_DIRECT_OUTPUT 1)
target_link_libraries(airspyhf-static libusb pthreads)