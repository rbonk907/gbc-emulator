# Manually create a list of source files because CMake
# documentation doesn't recommend using GLOB
set(SOURCES ${PROJECT_SOURCE_DIR}/lib/emu_core.c)
list(APPEND SOURCES ${PROJECT_SOURCE_DIR}/lib/bus.c)
list(APPEND SOURCES ${PROJECT_SOURCE_DIR}/lib/cartridge.c)
list(APPEND SOURCES ${PROJECT_SOURCE_DIR}/lib/ppu.c)
list(APPEND SOURCES ${PROJECT_SOURCE_DIR}/lib/sm83_cpu.c)
list(APPEND SOURCES ${PROJECT_SOURCE_DIR}/lib/timer.c)

# create a list of header files
set(HEADERS ${PROJECT_SOURCE_DIR}/include/emu_core.h)
list(APPEND HEADERS ${PROJECT_SOURCE_DIR}/include/bus.h)
list(APPEND HEADERS ${PROJECT_SOURCE_DIR}/include/cartridge.h)
list(APPEND HEADERS ${PROJECT_SOURCE_DIR}/include/ppu.h)
list(APPEND HEADERS ${PROJECT_SOURCE_DIR}/include/sm83_cpu.h)
list(APPEND HEADERS ${PROJECT_SOURCE_DIR}/include/timer.h)
list(APPEND HEADERS ${PROJECT_SOURCE_DIR}/include/common.h)

add_library(emulator STATIC ${SOURCES} ${HEADERS})
target_include_directories(emulator PUBLIC ${PROJECT_SOURCE_DIR}/include)

# if(WIN32)
# ...
# else()
target_include_directories(emulator PUBLIC ${SDL2_INLCUDE_DIR})
target_link_libraries(emulator PUBLIC ${SDL2_LIBRARY})
target_link_libraries(emulator PUBLIC ${SDL2_TFF_LIBRARY})
# endif()

include_directories("/usr/local/include")
include_directories(${SDL2_INCLUDE_DIRS})
target_link_libraries(emulator ${SDL2_LIBRARIES})
target_link_libraries(emulator ${SDL2_TFF_LIBRARIES})