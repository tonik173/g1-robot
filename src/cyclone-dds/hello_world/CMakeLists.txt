cmake_minimum_required(VERSION 3.16)
project(helloworld LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)

set(CMAKE_PREFIX_PATH "/home/kaan/cyclone-dds")
find_package(CycloneDDS-CXX REQUIRED)

idlcxx_generate(TARGET helloworlddata FILES hello_world_data.idl WARNINGS no-implicit-extensibility)

add_executable(HelloworldPublisher publisher.cpp)
add_executable(HelloworldSubscriber subscriber.cpp)

target_link_libraries(HelloworldPublisher CycloneDDS-CXX::ddscxx helloworlddata)
target_link_libraries(HelloworldSubscriber CycloneDDS-CXX::ddscxx helloworlddata)


