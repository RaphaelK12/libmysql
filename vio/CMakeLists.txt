# Copyright (C) 2006 MySQL AB
# 
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; version 2 of the License.
# 
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA

set ( VIO_SOURCES vio.c viosocket.c viossl.c viosslfactories.c )

if ( NOT SOURCE_SUBLIBS )
  set ( CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -D_DEBUG -DSAFEMALLOC -DSAFE_MUTEX" )
  set ( CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -D_DEBUG -DSAFEMALLOC -DSAFE_MUTEX" )

  add_definitions ( -DUSE_SYMDIR )
  include_directories ( ${CMAKE_SOURCE_DIR}/include ${CMAKE_SOURCE_DIR}/extlib/yassl/include )

  add_library ( vio STATIC ${VIO_SOURCES} )

  if ( SOCKET_LIBRARY )
    target_link_libraries ( vio ${SOCKET_LIBRARY} )
  endif ( SOCKET_LIBRARY )

endif ( NOT SOURCE_SUBLIBS )
