cmake_minimum_required (VERSION 3.7.2)

set(prefix "/usr/local")
set(PREFIX "/usr/local")
set(LIBEVENT_INCLUDE "-I${PREFIX}/include/ -I/usr/local/include/")
set(INCFLAGS "-Isrc -Isrc/apps/common -Isrc/server -Isrc/client -Isrc/client++ ${LIBEVENT_INCLUDE}")

set(TOP_MOST_ROOT ${CMAKE_CURRENT_SOURCE_DIR})

set(COMMON_DEFINES
    TURN_HAS_DAEMON 
    INSTALL_PREFIX=/usr/local
    TURNDB=/usr/local/var/db/turndb
    TURN_NO_PQ
    TURN_NO_MYSQL
    TURN_NO_MONGO
    TURN_NO_HIREDIS
)

set(COMMON_CFLAGS
    -g  -Wall -Wno-deprecated-declarations -Wextra -Wformat-security -Wnested-externs -Wstrict-prototypes
    -Wmissing-prototypes -Wpointer-arith -Wcast-qual
)

add_subdirectory(src/server)
add_subdirectory(src/client)
add_subdirectory(src/apps/common)
add_subdirectory(src/apps/relay)
