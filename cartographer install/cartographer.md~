#Ubuntu 14.04 环境下在ROS安装测试Cartographer#
##实验说明##
该安装和测试是基于[hitcm博主](http://www.cnblogs.com/hitcm/p/5939507.html)的相关博客进行修改，根据自己的实验平台测试可以通过，建议大家可以看看hitcm的博客。  
实验步骤中的源码也属于hitcm所有，这里只是给出具体的步骤。  

##实验环境##
- Ubuntu 14.04
- 请务必确保电脑可以联网

##安装过程##
- 安装依赖项：  
  
        sudo apt-get install -y google-mock libboost-all-dev  libeigen3-dev libgflags-dev libgoogle-glog-dev liblua5.2-dev libprotobuf-dev  libsuitesparse-dev libwebp-dev ninja-build protobuf-compiler python-sphinx  ros-indigo-tf2-eigen libatlas-base-dev libsuitesparse-dev liblapack-dev  
- 首先安装ceres solver,这里直接使用hitcm的代码，先在home目录下新建文件夹，命名为catkin_ws,打开终端进入(cd)该文件的目录下，执行以下代码：   

        git clone https://github.com/hitcm/ceres-solver-1.11.0.git  
- 执行之后，打开catkin_ws文件夹，可以看到名字为ceres-solver-1.11.0的文件夹，打开并新建文件夹build,在终端进入到该目录下（新建文件夹也可以在终端进行），执行以下指令：  
  
        cd ceres-solver-1.11.0/build  
- 在该目录下依次执行以下指令：  

        cmake
        make
        sudo make install
- 接着安装cartographer,在catkin_ws下新建文件夹，我的命名为cat，随后在终端进入该目录下，执行以下指令：  

        git clone https://github.com/hitcm/cartographer.git   
- 同样的，执行结束后可以看到一个cartographer的文件夹，在里面新建build文件夹，并在终端进入该路径下：  

        cd cartographer/build
- 进入后，依次执行以下指令：  

        cmake
        make 
        sudo make install
- 安装cartographer——ros，进入catkin_ws的src目录下，执行以下指令：  


        git clone https://github.com/hitcm/cartographer_ros.git  

- 在catkin_ws下执行指令：

        catkin_make
- 数据下载测试，我的方法是用迅雷下载到本地再复制到Ubuntu：

        https://storage.googleapis.com/cartographer-public-data/bags/backpack_2d/cartographer_paper_deutsches_museum.bag
由于数据包有8G的和4G，这里选了较小的，只是用来测试。
- 下载完成并复制到Ubuntu后，在终端执行指令：

        roslaunch cartographer_ros demo_backpack_2d.launch bag_filename:=${HOME}/Downloads/cartographer_paper_deutsches_museum.bag
执行指令后如果没有错误提示，就可以看到下面的正确图示。
- 正确测试结果图示：
  - 整体缩小图：
  ![picture1](http://p1.bqimg.com/567571/0a6cde9ad01e97e3.png)
  - 包含相关数据图：
  ![picture2](http://p1.bqimg.com/567571/912b84fdd15b2c2d.png)
  - 整体放大图：
  ![picyure3](http://p1.bqimg.com/567571/d46dd274f17cd41b.png)  

至此，安装和测试就完成了。
##错误总结##
在进行安装cartographer时没有新建文件夹，直接放在了src下面，在进行测试的时候会报错，建议新建一个文件夹存放安装需要的一大堆文件。  
按照参考的博客一般都是可以完成配置的，也没遇到奇奇怪怪的问题，如果有，那就是在安装某一步时出错但被自己忽略掉了=。= ，这样的话，就需要重新来了（至少我是重新来了一遍）。
##实验总结##
配置实验也不是很难，一定要细心，特别是执行make,sudo make install指令的时候，看到有错误提示或者failed字样，就需要检查一下，要不到最后出来一堆错误就GG了。  
最后，希望每个配置该实验的小伙伴都能成功:)