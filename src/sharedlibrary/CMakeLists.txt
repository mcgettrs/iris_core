 #
 # Copyright 2012 The Iris Project Developers. See the
 # COPYRIGHT file at the top-level directory of this distribution
 # and at http://www.softwareradiosystems.com/iris/copyright.html.
 #
 # This file is part of the Iris Project.
 #
 # Iris is free software: you can redistribute it and/or modify
 # it under the terms of the GNU Lesser General Public License as
 # published by the Free Software Foundation, either version 3 of
 # the License, or (at your option) any later version.
 #
 # Iris is distributed in the hope that it will be useful,
 # but WITHOUT ANY WARRANTY; without even the implied warranty of
 # MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 # GNU Lesser General Public License for more details.
 #
 # A copy of the GNU Lesser General Public License can be found in
 # the LICENSE file in the top-level directory of this distribution
 # and at http://www.gnu.org/licenses/.
 #

########################################################################
# Setup Dependencies
########################################################################
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR})

########################################################################
# Build the library from source files
########################################################################
IF(WIN32)
  ADD_LIBRARY(sharedlibrary SharedLibrary_windows.cpp)
ELSE(WIN32)
  FIND_PACKAGE(DL REQUIRED)
  INCLUDE_DIRECTORIES(${DL_INCLUDE_DIRS})
  ADD_LIBRARY(sharedlibrary STATIC SharedLibrary_posix.cpp)
  IRIS_SET_PIC(sharedlibrary)
  TARGET_LINK_LIBRARIES(sharedlibrary ${DL_LIBRARIES})
ENDIF(WIN32)
