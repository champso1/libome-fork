set(ome_sources
  ome/integration_engine_gsl.cpp
  ome/AqqQNSEven.cpp
  ome/AqqQNSOdd.cpp
  ome/AQqPS.cpp
  ome/AQqPSs.cpp
  ome/AgqQ.cpp
  ome/AggQ.cpp
  ome/AqgQ.cpp
  ome/AqqQPS.cpp
  ome/AQg.cpp
  ome/polAqqQNSEven.cpp
  ome/polAqqQNSOdd.cpp
  ome/polAQqPS.cpp
  ome/polAQqPSs.cpp
  ome/polAgqQ.cpp
  ome/polAggQ.cpp
  ome/polAqgQ.cpp
  ome/polAqqQPS.cpp
  ome/polAQg.cpp)
set(ome_headers
  ome/functions.h
  ome/integration_engine.h
  ome/integration_engine_gsl.h
  ome/laurent_polynomial.h
  ome/mellin.h
  ome/ome.h
  ome/ome_type_aliases.h
  ome/piecewise.h
  ome/rpd_distribution.h
  ome/traits.h
  ome/AqqQNSEven.h
  ome/AqqQNSOdd.h
  ome/AQqPS.h
  ome/AQqPSs.h
  ome/AgqQ.h
  ome/AggQ.h
  ome/AqgQ.h
  ome/AqqQPS.h
  ome/AQg.h
  ome/polAqqQNSEven.h
  ome/polAqqQNSOdd.h
  ome/polAQqPS.h
  ome/polAQqPSs.h
  ome/polAgqQ.h
  ome/polAggQ.h
  ome/polAqgQ.h
  ome/polAqqQPS.h
  ome/polAQg.h)

add_library(ome STATIC)
target_sources(ome
  PRIVATE ${ome_sources})
target_sources(ome PUBLIC
  FILE_SET ome_headers
  TYPE HEADERS
  BASE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}
  FILES ${ome_headers})

target_include_directories(ome PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
  $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>)
target_link_libraries(ome PUBLIC GSL::gsl)

