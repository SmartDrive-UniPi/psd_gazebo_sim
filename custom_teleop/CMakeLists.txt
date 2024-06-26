cmake_minimum_required(VERSION 3.8)
project(custom_teleop)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(SDL2 REQUIRED)

include_directories(include)

add_executable(custom_teleop_keyboard src/custom_teleop_keyboard.cpp)
ament_target_dependencies(custom_teleop_keyboard rclcpp std_msgs)

add_executable(custom_teleop_gamepad src/custom_teleop_gamepad.cpp)
ament_target_dependencies(custom_teleop_gamepad rclcpp std_msgs SDL2)
target_link_libraries(custom_teleop_gamepad SDL2::SDL2) 

add_executable(custom_teleop_logitech src/custom_teleop_logitech.cpp)
ament_target_dependencies(custom_teleop_logitech rclcpp std_msgs SDL2)
target_link_libraries(custom_teleop_logitech SDL2::SDL2) 



install(TARGETS custom_teleop_logitech custom_teleop_keyboard custom_teleop_gamepad DESTINATION lib/${PROJECT_NAME})

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
