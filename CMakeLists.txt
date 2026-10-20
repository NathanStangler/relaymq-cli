cmake_minimum_required(VERSION 3.25)
project(relaymq-cli
    VERSION 1.0.0
    DESCRIPTION "Command line interface for RelayMQ"
    LANGUAGES CXX
)

set(CMAKE_CXX_STANDARD 26)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_compile_options(
    -Wall
    -Wextra
    -Wpedantic
    -Wconversion
    -Wshadow
    -Wnon-virtual-dtor
)

if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/../relaymq-cpp/CMakeLists.txt")
    add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/../relaymq-cpp" relaymq-cpp)
else()
    include(FetchContent)
    FetchContent_Declare(
        relaymq_cpp
        GIT_REPOSITORY https://github.com/NathanStangler/relaymq-cpp.git
        GIT_TAG main
    )
    FetchContent_MakeAvailable(relaymq_cpp)
endif()

add_executable(relay-cli
    src/cli_main.cpp
)

target_link_libraries(relay-cli PRIVATE
    relaymq::client
)
