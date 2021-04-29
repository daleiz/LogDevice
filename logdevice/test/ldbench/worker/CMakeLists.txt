
auto_sources(hfiles "*.h" RECURSE "${LOGDEVICE_TEST_DIR}/ldbench/worker")
auto_sources(files "*.cpp" RECURSE "${LOGDEVICE_TEST_DIR}/ldbench/worker")

REMOVE_MATCHES_FROM_LISTS(files hfiles
  MATCHES
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/KafkaClient.cpp"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/KafkaClient.h"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/KafkaClientHolderTest.cpp"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/KafkaClientTest.cpp"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/KafkaReader.cpp"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/KafkaReader.h"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/OptionsModule.cpp"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/BenchStatsHolderTest.cpp"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/BenchStatsTest.cpp"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/ClientHolderIntegrationTest.cpp"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/FileBasedEventStoreTest.cpp"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/FileBasedStatsStoreTest.cpp"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/LogDeviceClientTest.cpp"
    "${LOGDEVICE_TEST_DIR}/ldbench/worker/LogDeviceReaderTest.cpp"
    
)

add_executable(ldbench ${hfiles} ${files})

target_link_libraries(ldbench
  ldclient
  common
  ${LOGDEVICE_EXTERNAL_DEPS})

