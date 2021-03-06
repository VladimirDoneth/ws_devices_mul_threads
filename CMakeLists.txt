cmake_minimum_required(VERSION 3.13)
project(ws_devices_2)

set(CMAKE_CXX_STANDARD 20)

add_executable(ws_devices_2 main2.cpp
        lib_i2c/i2c_driver.h lib_i2c/i2c_driver.cpp
        lib_mpu6050/mpu6050_drive.h lib_mpu6050/mpu6050_drive.cpp
        lib_bme280/BME280RawData.h lib_bme280/BME280Data.h lib_bme280/BME280CalibrationData.h lib_bme280/bme280.h lib_bme280/bme280.cpp
        web_sockets/WebServer.h web_sockets/WebServer.cpp
        web_sockets/my_web_server_worker.h web_sockets/my_web_server_worker.cpp
        lib_ssd1306/oled_fonts.h lib_ssd1306/ssd1306_driver.h lib_ssd1306/ssd1306_driver.cpp
        lib_mqtt_worker/my_mqtt_worker.h lib_mqtt_worker/my_mqtt_worker.cpp
        web_sockets/lib_my_event_handler/delegate_ws.cpp web_sockets/lib_my_event_handler/delegate_ws.h web_sockets/lib_my_event_handler/event_ws.cpp web_sockets/lib_my_event_handler/event_ws.h web_sockets/lib_my_event_handler/handler_ws.h
        processing_with_interrupt.h processing_with_interrupt.cpp)

target_link_libraries(ws_devices_2 seasocks "${ZLIB_LIBRARIES}")
target_link_libraries(ws_devices_2 pthread z)

target_link_libraries(ws_devices_2 paho-mqtt3c)
target_link_libraries(ws_devices_2 paho-mqttpp3)

add_custom_command(TARGET ws_devices_2 POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${PROJECT_SOURCE_DIR}/src/server_files $<TARGET_FILE_DIR:ws_devices_2>/src/server_files)