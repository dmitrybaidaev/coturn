project(main_relay_server C)

set(TARGET main_relay_server)

add_executable(${TARGET}
    dtls_listener.c
    netengine.c
    libtelnet.c
    turn_admin_server.c
    mainrelay.c
    tls_listener.c
    turn_ports.c
    ns_ioalib_engine_impl.c
    userdb.c
    http_server.c

    dbdrivers/dbd_pgsql.c
    dbdrivers/dbd_mysql.c
    dbdrivers/dbd_redis.c
    dbdrivers/dbd_mongo.c
    dbdrivers/dbd_sqlite.c
    dbdrivers/dbdriver.c
)

target_include_directories(${TARGET}
    PUBLIC
    ${LIBEVENT_INCLUDE}
    ${INCFLAGS}
    /usr/local/include


    ${TOP_MOST_ROOT}/include/turn
    ${TOP_MOST_ROOT}/include/turn/client
    .
    ${TOP_MOST_ROOT}/src/apps/common
    ${TOP_MOST_ROOT}/src/server
)

target_compile_definitions(${TARGET}
    PUBLIC
    ${COMMON_DEFINES}
)

target_compile_options(${TARGET}
    PRIVATE
    ${COMMON_CFLAGS}
)

target_link_libraries(${TARGET}
    -lrt -lnsl -lresolv -pthread -lcrypto -lssl -levent_core -levent_extra -levent_openssl
    -levent_pthreads -lsqlite3
    -Wl,-rpath,/usr/local/lib/

    -L${TOP_MOST_ROOT}/src/server
    -L${TOP_MOST_ROOT}/src/client
    -L${TOP_MOST_ROOT}/src/apps/common
    -lcoturn_server
    -lturn_utils
    -lturn_client
)
