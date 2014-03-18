project( gw_miner )
cmake_minimum_required( VERSION 2.8.10 )

IF( WIN32 )
  ADD_DEFINITIONS( -DWIN32 )
  ADD_DEFINITIONS( -DNOMINMAX )
  ADD_DEFINITIONS( -D_SCL_SECURE_NO_WARNINGS )
  ADD_DEFINITIONS( -D_WIN32_WINNT=0x0501 )
  ADD_DEFINITIONS( -D_CRT_SECURE_NO_WARNINGS )
  ADD_DEFINITIONS( -DWIN32)
  ADD_DEFINITIONS( -D_WIN32_WINNT=0x0501 )
  ADD_DEFINITIONS( -DLEVELDB_PLATFORM_WINDOWS )
  # Activate C++ exception handling
  IF (NOT CMAKE_CXX_FLAGS MATCHES "/EHsc")
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /EHsc")    
  ENDIF()
  #boost
  SET( Boost_INCLUDE_DIR $ENV{BOOST_ROOT} )

ELSE(WIN32)

  MESSAGE(status "Compiling on UNIX")
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x -Wall -Wno-unused-local-typedefs -fmax-errors=3 -msse4.2" ) 
  SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99 -Wall -Wno-unused-local-typedefs -fmax-errors=3 -msse4.2" )
  #SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x -Wall -Wno-unused-local-typedefs" ) 
  #SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99 -Wall -Wno-unused-local-typedefs" )
  SET(Boost_USE_STATIC_LIBS ON)
  FIND_PACKAGE(Boost 1.54 REQUIRED COMPONENTS thread date_time system filesystem program_options signals serialization chrono unit_test_framework context coroutine) 

 IF( NOT APPLE )
      SET( pthread pthread )
      SET( rt rt )
 ENDIF( NOT APPLE )
ENDIF(WIN32)

FIND_PACKAGE( OpenSSL )
include_directories( ${OPENSSL_INCLUDE_DIR} )
include_directories( ${Boost_INCLUDE_DIR} )
SET( ALL_OPENSSL_LIBRARIES ${OPENSSL_LIBRARIES} ${SSL_EAY_RELEASE} ${LIB_EAY_RELEASE})

include_directories( fc/include )
include_directories( sphlib-3.0/c)

add_subdirectory(fc)

add_executable( pool_miner pool_miner.cpp stcp_socket.cpp momentum.cpp bitcoin.cpp sphlib-3.0/c/sha2big.c )
target_link_libraries( pool_miner fc ${Boost_COROUTINE_LIBRARY} ${BOOST_LIBRARIES} ${pthread} ${rt})
