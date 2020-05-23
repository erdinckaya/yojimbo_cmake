cmake_minimum_required(VERSION 3.15)
project(yojimbo)

set(CMAKE_CXX_STANDARD 14)

find_package(unofficial-sodium CONFIG REQUIRED)

include_directories(netcode.io reliable.io)

find_path(MBEDTLS_INCLUDE_DIRS mbedtls/ssl.h)
include_directories(${MBEDTLS_INCLUDE_DIRS})

if (UNIX)
    find_library(MBEDTLS_LIBRARY libmbedtls.a)
    find_library(MBEDX509_LIBRARY libmbedx509.a)
    find_library(MBEDCRYPTO_LIBRARY libmbedcrypto.a)
elseif (WIN32)
    find_library(MBEDTLS_LIBRARY libmbedtls.lib)
    find_library(MBEDX509_LIBRARY libmbedx509.lib)
    find_library(MBEDCRYPTO_LIBRARY libmbedcrypto.lib)
endif ()

link_libraries(${MBEDTLS_LIBRARY})
link_libraries(${MBEDX509_LIBRARY})
link_libraries(${MBEDCRYPTO_LIBRARY})


add_library(${PROJECT_NAME}
        yojimbo.cpp yojimbo.h
        netcode.io/netcode.c netcode.io/netcode.h
        reliable.io/reliable.c reliable.io/reliable.h
        tlsf/tlsf.c tlsf/tlsf.c)
target_link_libraries(${PROJECT_NAME}
        ${MBEDTLS_LIBRARY} ${MBEDX509_LIBRARY} ${MBEDCRYPTO_LIBRARY} unofficial-sodium::sodium)
