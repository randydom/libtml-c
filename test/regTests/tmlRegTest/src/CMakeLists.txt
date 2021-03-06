#  libTML:  A BEEP based Messaging Suite
#  Copyright (C) 2015 wobe-systems GmbH
#
#  This program is free software; you can redistribute it and/or
#  modify it under the terms of the GNU Lesser General Public License
#  as published by the Free Software Foundation; either version 2.1
#  of the License, or (at your option) any later version.
#
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
#  Lesser General Public License for more details.
#
#  You should have received a copy of the GNU Lesser General Public
#  License along with this program; if not, write to the Free
#  Software Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA
#  02111-1307 USA
#  
#  You may find a copy of the license under this software is released
#  at COPYING file. This is LGPL software: you are welcome to develop
#  proprietary applications using this library without any royalty or
#  fee but returning back any change, improvement or addition in the
#  form of source code, project image, documentation patches, etc.
#
#  For professional support contact us:
#
#    wobe-systems GmbH
#    support@libtml.org
# 
# Contributors:
#    wobe-systems GmbH

#set(CMAKE_VERBOSE_MAKEFILE on)

#######################################################
## Common src path
#######################################################
set(COMMON_INCLUDE_PATH ../../../../common/src)
set(SIDEX_INCLUDE_PATH ../../../../sidex/src)
set(TML_INCLUDE_PATH ../../../../tml/src)
set(TMLTLS_INCLUDE_PATH ../../../../tml-tls/src)
set(AXL_INCLUDE_PATH2 ../../${AXLINCLUDE})
set(VORTEX_INCLUDE_PATH2 ../../${VORTEXINCLUDE})

set(TARGETNAME tmlRegTest)

#######################################################
## Windows 32 bit / MinGW build
#######################################################
if (${TML_TARGET_PLATFORM} STREQUAL win_x86-32_mingw)
  ADD_DEFINITIONS("-DSIDEX_UNICODE -DTML_UNICODE -DMINGW_BUILD")
  ADD_DEFINITIONS("-std=c++0x")
  ADD_DEFINITIONS("-fpermissive")
  set(IS64BIT false)
  set(AXLLIB libaxl.lib)
  set(VORTEXLIB libvortex-1.1.lib)

  ADD_DEFINITIONS ("-m32")
  set(CMAKE_CXX_FLAGS "-m32")
endif (${TML_TARGET_PLATFORM} STREQUAL win_x86-32_mingw)

#######################################################
## Windows 64 bit / MinGW build
#######################################################
if (${TML_TARGET_PLATFORM} STREQUAL win_x86-64_mingw)
  ADD_DEFINITIONS("-DSIDEX_UNICODE -DTML_UNICODE -DMINGW_BUILD")
  ADD_DEFINITIONS("-std=c++0x")
  ADD_DEFINITIONS("-fpermissive")
  set(IS64BIT true)
  set(AXLLIB libaxl.lib)
  set(VORTEXLIB libvortex-1.1.lib)

  ADD_DEFINITIONS ("-m64")
  set(CMAKE_CXX_FLAGS "-m64")
endif (${TML_TARGET_PLATFORM} STREQUAL win_x86-64_mingw)

#######################################################
## Windows 32 bit
#######################################################
if (${TML_TARGET_PLATFORM} STREQUAL win_x86-32)
  ADD_DEFINITIONS("-DSIDEX_UNICODE -DTML_UNICODE")
  set(IS64BIT false)
  set(AXLLIB libaxl.lib)
  set(VORTEXLIB libvortex-1.1.lib)
endif (${TML_TARGET_PLATFORM} STREQUAL win_x86-32)

#######################################################
## Windows 64 bit
#######################################################
if (${TML_TARGET_PLATFORM} STREQUAL win_x86-64)
  ADD_DEFINITIONS("-DSIDEX_UNICODE -DTML_UNICODE")
  set(IS64BIT true)
  set(AXLLIB libaxl.lib)
  set(VORTEXLIB libvortex-1.1.lib)
endif (${TML_TARGET_PLATFORM} STREQUAL win_x86-64)

#######################################################
## LINUX 32 bit
#######################################################
if (${TML_TARGET_PLATFORM} STREQUAL linux_x86-32)
  set(IS64BIT false)
  set(AXLLIB libaxl.so)
  set(VORTEXLIB libvortex-1.1.so)

  ADD_DEFINITIONS ("-std=c++0x")
  ADD_DEFINITIONS("-m32")
  ADD_DEFINITIONS("-DLINUX -DSIDEX_UNICODE -DTML_UNICODE -DGCC4")
  set(CMAKE_CXX_FLAGS "-m32")
endif (${TML_TARGET_PLATFORM} STREQUAL linux_x86-32)

#######################################################
## LINUX 64 bit
#######################################################
if (${TML_TARGET_PLATFORM} STREQUAL linux_x86-64)
  set(IS64BIT true)
  set(AXLLIB libaxl.so)
  set(VORTEXLIB libvortex-1.1.so)

  ADD_DEFINITIONS ("-std=c++0x")
  ADD_DEFINITIONS("-m64")
  ADD_DEFINITIONS("-DLINUX -DSIDEX_UNICODE -DTML_UNICODE -DGCC4")
  set(CMAKE_CXX_FLAGS "-m64")
endif (${TML_TARGET_PLATFORM} STREQUAL linux_x86-64)

#######################################################
## FreeBSD / 32 bit
#######################################################
if (${TML_TARGET_PLATFORM} STREQUAL freeBSD_x86-32)
  set(IS64BIT false)
  set(AXLLIB libaxl.so)
  set(VORTEXLIB libvortex-1.1.so)

  ADD_DEFINITIONS ("-std=c++0x -fpermissive")
  ADD_DEFINITIONS("-m32")
  ADD_DEFINITIONS("-DLINUX -DFREE_BSD -DSIDEX_UNICODE -DTML_UNICODE -DGCC4")
  set(CMAKE_CXX_FLAGS "-m32")
endif (${TML_TARGET_PLATFORM} STREQUAL freeBSD_x86-32)

#######################################################
## FreeBSD / 64 bit
#######################################################
if (${TML_TARGET_PLATFORM} STREQUAL freeBSD_x86-64)
  set(IS64BIT true)
  set(AXLLIB libaxl.so)
  set(VORTEXLIB libvortex-1.1.so)

  ADD_DEFINITIONS ("-std=c++0x -fpermissive")
  ADD_DEFINITIONS("-m64")
  ADD_DEFINITIONS("-DLINUX -DFREE_BSD -DSIDEX_UNICODE -DTML_UNICODE -DGCC4")
  set(CMAKE_CXX_FLAGS "-m64")
endif (${TML_TARGET_PLATFORM} STREQUAL freeBSD_x86-64)

#######################################################
## OSX 32 bit
#######################################################
if (${TML_TARGET_PLATFORM} STREQUAL osx_x86-32)
  set(IS64BIT false)
  set(AXLLIB libaxl.0.dylib)
  set(VORTEXLIB libvortex-1.1.dylib)

  ADD_DEFINITIONS ("-std=c++11")
  ADD_DEFINITIONS("-arch i386")
  ADD_DEFINITIONS("-DLINUX -DOS_X -DSIDEX_UNICODE -DTML_UNICODE")
  set(CMAKE_CXX_FLAGS "-arch i386")
endif (${TML_TARGET_PLATFORM} STREQUAL osx_x86-32)

#######################################################
## OSX 64 bit
#######################################################
if (${TML_TARGET_PLATFORM} STREQUAL osx_x86-64)
  set(IS64BIT true)
  set(AXLLIB libaxl.0.dylib)
  set(VORTEXLIB libvortex-1.1.dylib)

  ADD_DEFINITIONS ("-std=c++11")
  ADD_DEFINITIONS("-arch x86_64")
  ADD_DEFINITIONS("-DLINUX  -DOS_X -DSIDEX_UNICODE -DTML_UNICODE")
  set(CMAKE_CXX_FLAGS "-arch x86_64")
endif (${TML_TARGET_PLATFORM} STREQUAL osx_x86-64)

#######################################################
## LINUX ARM32
#######################################################
if (${TML_TARGET_PLATFORM} STREQUAL linux_arm32)
  set(IS64BIT false)
  set(AXLLIB libaxl.so)
  set(VORTEXLIB libvortex-1.1.so)

  ADD_DEFINITIONS ("-std=c++0x")
  ADD_DEFINITIONS("-DLINUX -DSIDEX_UNICODE -DTML_UNICODE" -DGCC4)
endif (${TML_TARGET_PLATFORM} STREQUAL linux_arm32)

#######################################################

if (${IS64BIT} STREQUAL false)
  set(TARGETNAME_LOCAL  ${TARGETNAME})
else (${IS64BIT} STREQUAL false)
  set(TARGETNAME_LOCAL ${TARGETNAME}64)
endif (${IS64BIT} STREQUAL false)

set(TARGET ${TARGETNAME_LOCAL})
set	 (TEST_SOURCES_HEADER
  "TestingForReturns.h"
  "TestingProcess.h"
  "TestParams.h"
  "TmlConnectionTester.h"
  "TmlCore.h"
  "TmlMultipleListenersTester.h"
  "tmlrt_Connections.h"
  "tmlrt_MultipleListeners.h"
  "tmlrt_SendingCommands.h"
  "tmlrt_TLS.h"
  "tmlrt_Utils.h"
  "TmlSendingCommandsTester.h"
  "TmlTester.h"
  "TmlTLSTester.h"
  "tmlrt_GetVersion.h")
set  (TEST_SOURCES
  "TestingForReturns.cpp"
  "TestingProcess.cpp"
  "TestParams.cpp"
  "TmlConnectionTester.cpp"
  "TmlCore.cpp"
  "TmlMultipleListenersTester.cpp"
  "tmlrt.cpp"
  "tmlrt_Connections.cpp"
  "tmlrt_MultipleListeners.cpp"
  "tmlrt_SendingCommands.cpp"
  "tmlrt_TLS.cpp"
  "tmlrt_Utils.cpp"
  "TmlSendingCommandsTester.cpp"
  "TmlTester.cpp"
  "TmlTLSTester.cpp"
  "tmlrt_GetVersion.cpp"
  "../../../../common/src/unicode.cpp")

add_executable(${TARGETNAME_LOCAL} 
               ${TEST_SOURCES_HEADER} ${TEST_SOURCES})

#######################################################
## Include- directories:
#######################################################
if (AXL_INCLUDE_PATH2)
  INCLUDE_DIRECTORIES (${AXL_INCLUDE_PATH2})
endif()
if (VORTEX_INCLUDE_PATH2)
  INCLUDE_DIRECTORIES (${VORTEX_INCLUDE_PATH2})
endif()
INCLUDE_DIRECTORIES (${AXLINCLUDE})
INCLUDE_DIRECTORIES (${VORTEXINCLUDE})
INCLUDE_DIRECTORIES (${SIDEX_INCLUDE_PATH})
INCLUDE_DIRECTORIES (${TML_INCLUDE_PATH})
INCLUDE_DIRECTORIES (${TMLTLS_INCLUDE_PATH})
INCLUDE_DIRECTORIES (".")
INCLUDE_DIRECTORIES (${COMMON_INCLUDE_PATH})

#######################################################
## libraries
#######################################################
TARGET_LINK_LIBRARIES(${TARGET} ${SIDEXLIBNAME})
TARGET_LINK_LIBRARIES(${TARGET} ${TMLLIBNAME})
TARGET_LINK_LIBRARIES(${TARGET} ${TLSLIBNAME})
TARGET_LINK_LIBRARIES(${TARGET} ${AXLLIB})
TARGET_LINK_LIBRARIES(${TARGET} ${VORTEXLIB})
