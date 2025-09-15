cmake_minimum_required(VERSION 3.16)
project(throughput LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)

set(CMAKE_PREFIX_PATH "~/cyclone-dds")
find_package(CycloneDDS-CXX REQUIRED)

idlcxx_generate(TARGET RoundTrip_lib_cxx FILES round_trip.idl WARNINGS no-implicit-extensibility)

add_executable(RoundtripPing ping.cpp)
add_executable(RoundtripPong pong.cpp)

target_link_libraries(RoundtripPing RoundTrip_lib_cxx CycloneDDS-CXX::ddscxx)
target_link_libraries(RoundtripPong RoundTrip_lib_cxx CycloneDDS-CXX::ddscxx)