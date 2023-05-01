set(MAIN_SOURCES main.c)

# create a list of header files
set(HEADERS ${PROJECT_SOURCE_DIR}/include/emu_core.h)
list(APPEND HEADERS ${PROJECT_SOURCE_DIR}/include/bus.h)
list(APPEND HEADERS ${PROJECT_SOURCE_DIR}/include/cartridge.h)
list(APPEND HEADERS ${PROJECT_SOURCE_DIR}/include/ppu.h)
list(APPEND HEADERS ${PROJECT_SOURCE_DIR}/include/sm83_cpu.h)
list(APPEND HEADERS ${PROJECT_SOURCE_DIR}/include/timer.h)
list(APPEND HEADERS ${PROJECT_SOURCE_DIR}/include/common.h)

# executable   [name]  [source]   [source]
add_executable(gbc-emu ${HEADERS} ${MAIN_SOURCES})
target_link_libraries(gbc-emu emulator)
target_include_directories(gbc-emu PUBLIC ${PROJECT_SOURCE_DIR}/include)

message(STATUS "SDL Libraries: ${SDL2_LIBRARIES} - ${SDL2_LIBRARY}")
message(STATUS "SDL TTF Libraries: ${SDL_TTF_LIBRARIES} - ${SDL2_TTF_LIBRARY}")

install(TARGETS gbc-emu
RUNTIME DESTINATION bin
LIBRARY DESTINATION lib
ARCHIVE DESTINATION lib)


