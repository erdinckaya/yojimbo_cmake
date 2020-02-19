cmake_minimum_required(VERSION 3.15)
project(yojimbo)

set(CMAKE_CXX_STANDARD 14)

find_package(unofficial-sodium CONFIG REQUIRED)

include_directories(netcode.io reliable.io)

find_path(MBEDTLS_INCLUDE_DIRS mbedtls/ssl.h)
include_directories(${MBEDTLS_INCLUDE_DIRS})

find_library(MBEDTLS_LIBRARY libmbedtls.a)
link_libraries(${MBEDTLS_LIBRARY})
find_library(MBEDX509_LIBRARY libmbedx509.a)
link_libraries(${MBEDX509_LIBRARY})
find_library(MBEDCRYPTO_LIBRARY libmbedcrypto.a)
link_libraries(${MBEDCRYPTO_LIBRARY})



add_library(yojimbo
        yojimbo.cpp yojimbo.h
        netcode.io/netcode.c netcode.io/netcode.h
        reliable.io/reliable.c reliable.io/reliable.h
        tlsf/tlsf.c tlsf/tlsf.c)