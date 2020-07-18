cmake_minimum_required (VERSION 3.7.2)

project(coturn_server C)

set(TARGET coturn_server)

add_library(${TARGET} STATIC
    ns_turn_allocation.c
    ns_turn_maps.c
    ns_turn_maps_rtcp.c
    ns_turn_server.c
)

if(CMAKE_BUILD_TYPE STREQUAL "")
	message("${CMAKE_CURRENT_SOURCE_DIR}: CMAKE_BUILD_TYPE has not been set, force to Release")
	set(CMAKE_BUILD_TYPE "Release")
endif()

set(prefix "/usr/local")
set(PREFIX "/usr/local")
set(LIBEVENT_INCLUDE "-I${PREFIX}/include/ -I/usr/local/include/")
set(INCFLAGS "-Isrc -Isrc/apps/common -Isrc/server -Isrc/client -Isrc/client++ ${LIBEVENT_INCLUDE}")

set(TOP_MOST_ROOT ../..)

target_include_directories(${TARGET}
    PUBLIC
    ${LIBEVENT_INCLUDE}
    ${INCFLAGS}
    /usr/local/include

    .
    ../apps/common
    ${TOP_MOST_ROOT}/include/turn
    ${TOP_MOST_ROOT}/include/turn/client
)

target_compile_definitions(${TARGET}
    PUBLIC
    TURN_HAS_DAEMON 
    TURN_SCTP_INCLUDE=\"</usr/include/netinet/sctp.h>\"
    INSTALL_PREFIX=/usr/local
    TURNDB=/usr/local/var/db/turndb
    TURN_NO_PQ
    TURN_NO_MYSQL
    TURN_NO_MONGO
    TURN_NO_HIREDIS
)

target_compile_options(${TARGET}
    PRIVATE
    -g  -Wall -Wno-deprecated-declarations -Wextra -Wformat-security -Wnested-externs -Wstrict-prototypes
    -Wmissing-prototypes -Wpointer-arith -Wcast-qual
)

# target_link_libraries(${TARGET}
#     -lrt -lnsl -lresolv -pthread -lcrypto -lssl -levent_core -levent_extra -levent_openssl
#     -levent_pthreads -lsqlite3
#     -Wl,-rpath,/usr/local/lib/
#     -Wl,-rpath,/usr/local/lib/
#     -Wl,-rpath,/usr/local/lib
#     -L/usr/local/lib/ -L/usr/local/lib/
# )
