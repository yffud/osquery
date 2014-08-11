FILE(GLOB table_sources
  "generated/*.cpp"
  "manual/*.cpp"
)

ADD_LIBRARY(osquery_tables
  registry.cpp
  ${table_sources}
  examples/example.cpp
  networking/etc_hosts.cpp
  system/processes.cpp
)
TARGET_LINK_LIBRARIES(osquery_tables boost_filesystem)
TARGET_LINK_LIBRARIES(osquery_tables glog)
TARGET_LINK_LIBRARIES(osquery_tables osquery_filesystem)
TARGET_LINK_LIBRARIES(osquery_tables osquery_sqlite)
TARGET_LINK_LIBRARIES(osquery_tables "-Wl,-all_load")
TARGET_LINK_LIBRARIES(osquery_tables "-fobjc-arc -fobjc-link-runtime -framework Foundation")

ADD_EXECUTABLE(etc_hosts_tests networking/etc_hosts_tests.cpp)
TARGET_LINK_LIBRARIES(etc_hosts_tests gtest)
TARGET_LINK_LIBRARIES(etc_hosts_tests glog)
TARGET_LINK_LIBRARIES(etc_hosts_tests osquery_core)
TARGET_LINK_LIBRARIES(etc_hosts_tests osquery_database)
TARGET_LINK_LIBRARIES(etc_hosts_tests osquery_filesystem)
TARGET_LINK_LIBRARIES(etc_hosts_tests osquery_tables)