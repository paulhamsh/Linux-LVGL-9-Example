# Linux-LVGL-9-Example
Linux LVGL 9 Example

## Build instructions for lv_port_linux_frame_buffer

```
git clone https://github.com/lvgl/lv_port_linux_frame_buffer.git
cd lv_port_linux_frame_buffer/
git submodule update --init --recursive
```

Then ensure this line is in ```lv_conf.h```  

```
#define LV_USE_LINUX_FBDEV      1
```

Then edit ```CMakeFiles.txt``` to be like the example below:   

```
cmake_minimum_required(VERSION 3.10)
project(lvgl)

set(CMAKE_C_STANDARD 99)#C99 # lvgl officially support C99 and above
set(CMAKE_CXX_STANDARD 17)#C17
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

add_subdirectory(lvgl)
target_include_directories(lvgl PUBLIC ${PROJECT_SOURCE_DIR})

add_executable(main main.c mouse_cursor_icon.c)

#include(${CMAKE_CURRENT_LIST_DIR}/lvgl/tests/FindLibDRM.cmake)
#include_directories(${Libdrm_INCLUDE_DIRS})

#find_package(SDL2)
#find_package(SDL2_image)
#include_directories(${SDL2_INCLUDE_DIRS} ${SDL2_IMAGE_INCLUDE_DIRS})

#target_link_libraries(main lvgl lvgl::examples lvgl::demos lvgl::thorvg ${SDL2_LIBRARIES} ${SDL2_IMAGE_LIBRARIES} ${Libdrm_LIBRARIES} m pthread)

target_link_libraries(main lvgl lvgl::examples lvgl::demos lvgl::thorvg  m pthread)
add_custom_target (run COMMAND ${EXECUTABLE_OUTPUT_PATH}/main DEPENDS main)
```

This is just removing references to SDL and Libdrm.   

Then make:

```
mkdir build
cd build 
cmake ..
make -j
```

The resulting bin/main will run.

## Build instructions my code

Copy ```main.c``` and re-do the ```make -j```


