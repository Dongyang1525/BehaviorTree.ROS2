# BehaviorTree.ROS2
[![Test](https://github.com/BehaviorTree/BehaviorTree.ROS2/actions/workflows/test.yml/badge.svg)](https://github.com/BehaviorTree/BehaviorTree.ROS2/actions/workflows/test.yml)

---
针对send_nav_goal导航任务取消导致决策崩溃，背后是RosActionNode 的节点无法被正确 halt，异常无法被处理，最终导致行为树被 shutdown的问题，我们保留原有 async_get_result(goal_handle_) 逻辑不变。
仅对 action_client->async_cancel_goal(goal_handle_) 增加 try-catch。
捕获 rclcpp_action::exceptions::UnknownGoalHandleError 后：
记录一条 WARN 日志
直接 return

修改：Simon_Von_Braun

---

This repository contains useful wrappers to use ROS2 and BehaviorTree.CPP together.

In particular, it provides a standard way to implement:

- Behavior Tree Executor with ROS Action interface.
- Action clients.
- Service Clients.
- Topic Subscribers.
- Topic Publishers.

Our main goals are:

- to minimize the amount of boilerplate.
- to make asynchronous Actions non-blocking.

# Documentation

- [ROS Behavior Wrappers](behaviortree_ros2/ros_behavior_wrappers.md)
- [TreeExecutionServer](behaviortree_ros2/tree_execution_server.md)
- [Sample Behaviors](btcpp_ros2_samples/README.md)

Note that this library is compatible **only** with:

- **BT.CPP** 4.6 or newer.
- **ROS2** Humble or newer.

Additionally, check **plugins.hpp** to see how to learn how to
wrap your Nodes into plugins that can be loaded at run-time.


## Acknowledgements

A lot of code is either inspired or copied from [Nav2](https://docs.nav2.org/).

For this reason, we retain the same license and copyright.
