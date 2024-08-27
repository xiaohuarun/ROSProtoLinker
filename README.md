# ROSProtoLinker
通过利用模板编程中的 C++ SFINAE，我修改了 roscpp_serialization 和 roscpp_traits。这使得 ROSProtoLinker 可以无缝支持 ROS 原生消息和 Protobuf 消息，增强了其兼容性和可扩展性。我是在dorcker中跑的这个代码，如果不使用dorcker也是可以的，你的操作系统需要安装protobuff和ros 20.04，就可以去跑一下我的代码。不过需要注意，我的cmakelist.txt会把message_serialization和message_traits复制到操作系统的ros原本的文本中，这样做我是为了跑一次就可以内置使用protobuff.

![这个是如何在ros接入proto的一个过程](https://github.com/xiaohuarun/ROSProtoLinker/blob/main/image/ROSProtoLinker.png)

# 使用方法
 1. 构造docker环境
    ``` shell
      cd ~/work/ros_protobuf_msg/docker/build
      docker build --network host -t ros_protobuf:noetic  -f ros_x86.dockerfile .
    ```
 2. 进入容器
  ``` shell
      cd ~/work/ros_protobuf_msg/docker/scripts
      #启动容器
      ./ros_docker_run.sh
      #进入容器
      ./ros_docker_into.sh
  ```
  3. 编译源代码
  ``` shell
      #创建build目录
      mkdir build
      cd build
      cmake ..
      make -j6
  ```
  4. 启动测试
   ``` shell
    cd /work
    source devel/setup.bash
    roscore &
    rosrun myproject pb_talker
   ```
   ``` shell
    cd ~/work/ros_protobuf_msg/docker/scripts
    #进入容器
    ./ros_docker_into.sh
    rosrun myproject pb_listener
   ```  
