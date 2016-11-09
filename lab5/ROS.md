#Ubuntu 14.04环境下配置ROS  

##实验环境##
- Ubuntu14.04
- 进行配置时要下载相关数据包，请确保有网
  
##实验步骤##
此次实验的所有步骤都来自[ROS.org](http://wiki.ros.org/jade/Installation/Ubuntu)(该网页为英文原网页)  
如果觉得英文有点难，可以查看该[中文网站ROS.org](http://wiki.ros.org/cn/jade/Installation/Ubuntu)  
  
##安装过程###
- 添加source.list,指令如下：  
       
          sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'   
- 添加keys,指令如下：  
  
           sudo apt-key adv --keyserver hkp://pool.sks-keyservers.net --recv-key 0xB01FA116  
- 安装
  - 首先确保虚拟机的Debian软件包索引是最新的：  
  
            sudo apt-get update  
  - 桌面完整版安装： 包含ROS、[rqt](http://wiki.ros.org/rqt)、[rviz](http://wiki.ros.org/rviz)、通用机器人函数库、2D/3D仿真器、导航以及2D/3D感知功能  
     
             sudo apt-get install ros-jade-desktop-full  
  - 初始化rosdep:  
    
             sudo rosdep init
             rosdep update  
  - 环境配置：如果每次打开一个新的终端时ROS环境变量都能够自动配置好（即添加到bash会话中），那将会方便很多  
  
             echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc
             source ~/.bashrc  
   - 如果你安装有多个ROS版本, ~/.bashrc 必须只能 source 你当  前使用版本所对应的 setup.bash。
   如果你只想改变当前终端下的环境变量，可以执行以下命令  
    
              source /opt/ros/jade/setup.bash  
   - 安装rosinatall:[rosinstall](http://wiki.ros.org/rosinstall) 是ROS中一个独立分开的常用命令行工具，它可以方便让你通过一条命令就可以给某个ROS软件包下载很多源码树。
   要在ubuntu上安装这个工具，请运行：  
  
              sudo apt-get install python-rosinstall  
- 至此，整个安装过程就结束了。接下里测试一下看看我们的安装是否成功！  
  
###测试ROS###
声明：以下测试教程和代码来源于[这里](http://www.th7.cn/system/lin/201504/103167.shtml)   
安装ROS成功后，在Beginner Tutorials有一个简单的示例程序  
  
- 打开一个终端，输入指令：  
                    
        roscore
  - 出现以下界面：  
  ![picture](https://github.com/guiguiw/ES2016_14353394/blob/master/1.png)
  
- 打开第二个终端，输入以下指令，开启一个小乌龟界面：  

         rosrun turtlesim turtlesim_node
  - 出现以下界面：
  ![picture2](https://github.com/guiguiw/ES2016_14353394/blob/master/2.png)
- 打开第三个终端，输入以下指令，接收键盘输入，控制小乌龟移动

        rosrun turtlesim turtle_teleop_key
- 选中最后打开的Terminal,键盘按下上下左右按键,可看到控制小乌龟移动.
   - 出现以下界面：
   ![](https://github.com/guiguiw/ES2016_14353394/blob/master/3.png)  
  （本图的乌龟和上图的不同，是因为第一次运行时没有让乌龟移动就关闭了窗口，再次打开时乌龟就变了样子。）
- 打开第四个终端，输入以下指令，可以看到ROS nodes以及Topic等图形展示：

        rosrun rqt_graph rqt_graph
   - 出现以下界面：
   ![picture3](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/22968833.jpg)
   由上图可看见，左右两边矩形为ROS node，中间连线上是Topic名称。  

至此，ROS配置就结束了，从测试中我们也可以看出安装是成功的。

##实验感想##
此次实验比较简单，都是按照教程来做，因为是个英语渣，所以就找了中文的网址对照着做，之前在做到2.1的时候会有如下报错：
![picture4](https://github.com/guiguiw/ES2016_14353394/blob/master/4.png)  
这里的2.1是用于获取安装包的源码，所以可以不用管这个，如果测试通过就说明成功了。


