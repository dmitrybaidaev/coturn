project(turn_client C)

set(TARGET turn_client)

add_library(${TARGET} STATIC
    ns_turn_msg_addr.c
    ns_turn_msg.c
    ns_turn_ioaddr.c
)

target_include_directories(${TARGET}
    PUBLIC
    ${LIBEVENT_INCLUDE}
    ${INCFLAGS}
    /usr/local/include

    .
    ${TOP_MOST_ROOT}/src
    ${TOP_MOST_ROOT}/src/apps/common
)

target_compile_definitions(${TARGET}
    PUBLIC
    ${COMMON_DEFINES}
)

target_compile_options(${TARGET}
    PRIVATE
    ${COMMON_CFLAGS}
)