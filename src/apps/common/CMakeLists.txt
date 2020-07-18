project(turn_utils C)

set(TARGET turn_utils)

add_library(${TARGET} STATIC
    stun_buffer.c
    ns_turn_utils.c
    hiredis_libevent2.c
    apputils.c
)

target_include_directories(${TARGET}
    PUBLIC
    ${LIBEVENT_INCLUDE}
    ${INCFLAGS}
    /usr/local/include

    .
    ../apps/common
    ${TOP_MOST_ROOT}/src/server
    ${TOP_MOST_ROOT}/include/turn
    ${TOP_MOST_ROOT}/include/turn/client
)

target_compile_definitions(${TARGET}
    PUBLIC
    ${COMMON_DEFINES}
)

target_compile_options(${TARGET}
    PRIVATE
    ${COMMON_CFLAGS}
)
