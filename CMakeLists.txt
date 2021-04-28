cmake_minimum_required(VERSION 3.5)
project(rb_msgs)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(trajectory_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)

set(ACT "action/Test.action"
        "action/ComputerVision.action"
        )

set(MSG "msg/RobotState.msg"
        "msg/AuboError.msg"

        "msg/Analog.msg"
        "msg/Digital.msg"
        "msg/GoalPoint.msg"
        "msg/IOState.msg"
        "msg/JointPose.msg"
        "msg/TrajectoryPoint.msg"
        "msg/Position.msg"
        "msg/Orientation.msg"
        "msg/Waypoint.msg"
        "msg/RobotEvent.msg"
        "msg/ToolIO.msg"
        "msg/ToolIOStatus.msg"
        "msg/DetectedObject.msg"
        )

set(SRV "srv/Test.srv"
        "srv/RobotModel.srv"
        "srv/GoHome.srv"
        "srv/Move.srv"
        "srv/GetIK.srv"
        "srv/MoveLine.srv"
        "srv/Gripper.srv"
        )

rosidl_generate_interfaces(${PROJECT_NAME}
        ${ACT}
        ${MSG}
        ${SRV}
        DEPENDENCIES
        builtin_interfaces
        std_msgs
        trajectory_msgs
        sensor_msgs
        geometry_msgs)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_export_dependencies(std_msgs)
ament_export_dependencies(sensor_msgs)
ament_export_dependencies(geometry_msgs)
ament_export_dependencies(rosidl_default_runtime)

ament_package()
