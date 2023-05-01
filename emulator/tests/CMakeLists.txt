include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

find_package(Check REQUIRED)
include_directories(${CHECK_INCLUDE_DIRS})
include_directories("/usr/local/include")
link_directories(${CHECK_LIBRARY_DIRS})

set(TEST_SOURCES check_gbc_emu.c)

add_executable(check_gbc_emu ${TEST_SOURCES})
target_link_libraries(check_gbc_emu emulator ${CHECK_LIBRARIES})
target_include_directories(check_gbc_emu PRIVATE ${PROJECT_SOURCE_DIR}/include)

find_program(DEBIAN "dpkg")
if(DEBIAN)
    target_link_libraries(check_gbc_emu check m rt pthread subunit)
endif(DEBIAN)

