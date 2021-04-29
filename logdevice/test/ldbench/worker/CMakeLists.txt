
auto_sources(hfiles "*.h" RECURSE "${LOGDEVICE_TEST_DIR}/ldbench/worker")
auto_sources(files "*.cpp" RECURSE "${LOGDEVICE_TEST_DIR}/ldbench/worker")

## REMOVE_MATCHES_FROM_LISTS(files hfiles
##   MATCHES
##     "/test/"
##     "/locallogstore/test/"
##     "/admincommands/"
##     "${LOGDEVICE_SERVER_DIR}/main.cpp"
##     "${LOGDEVICE_SERVER_DIR}/Server.cpp"
##     "${LOGDEVICE_SERVER_DIR}/Server.h"
##     "${LOGDEVICE_SERVER_DIR}/shutdown.h"
##     "${LOGDEVICE_SERVER_DIR}/shutdown.cpp"
## )

add_executable(ldbench ${hfiles} ${files})

target_link_libraries(ldbench
  ldclient
  common
  ${LOGDEVICE_EXTERNAL_DEPS})

