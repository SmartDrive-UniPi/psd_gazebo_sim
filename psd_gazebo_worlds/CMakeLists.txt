cmake_minimum_required(VERSION 3.8)
project(psd_gazebo_worlds)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)

install(DIRECTORY
  DESTINATION share/${PROJECT_NAME}
)

install(DIRECTORY
  world/
  DESTINATION share/${PROJECT_NAME}/worlds/
)

ament_package()
