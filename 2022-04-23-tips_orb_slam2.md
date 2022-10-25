1. 安装前准备
   
   ```bash
   vim cmake git gcc g++ libeigen3-dev(eigen)
   ```
   
2. 安装Pangolin
   
   - 依赖项：
   
   ```bash
   sudo apt install libglew-dev
   sudo apt install libboost-dev libboost-thread-dev libboost-filesystem-dev
   sudo apt install libpython2.7-dev
   ```
   
   - 流程
   
   ```bash
   git clone
   cd Pangolin
   git reset --hard v0.8(改为v0.5)
   mkdir build
   cd build
   cmake ..
   make -j12
   sudo make install
   ```
   
3. 安装OpenCV
   
   - 依赖项：
   
   ```bash
   sudo apt install build-essential libgtk2.0-dev libjpeg-dev libopenexr-dev libtbb-dev
   sudo apt install libavcodec-dev libavformat-dev libswscale-dev libtiff5-dev libvtk6-dev
   sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
   sudo apt update
   sudo apt install libjasper1 libjasper-dev
   ```
   
   - 流程
   
   ```bash
   cd opencv-3.4.5
   mkdir build
   cd build
	cmake ..
   make -j12
	sudo make install
	```
	
	- 配置环境变量
	
	```bash
	执行 sudo vim /etc/ld.so.conf.d/opencv.conf
	添加 /usr/local/lib
	执行 sudo ldconfig
	```
	
	- 执行
	
	```bash
	sudo vim /etc/bash.bashrc
	```
	
	- 添加
	
	```bash
	PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig
	export PKG_CONFIG_PATH
	```
	
	- 执行
	
	```bash
	source /etc/bash.bashrc
	sudo updatedb
	```
	
	- 测试
	
	```bash
	cd opencv-3.4.5/samples/cpp/example_cmake
	cmake .
	make
	./opencv_example
	```
	
4. 安装ORB_SLAM2
   
   ```bash
   git clone
   cd ORB_SLAM2
   sudo chmod +x build.sh
   ./build.sh
   ```
   
   ​	如果报usleep相关的错误则在对应的/src/.cc文件中加入#include <unistd.h>
   
5. 报错Pangolin could not be found because dependency Eigen3 could not be found.
   
   - 降低Pangolin版本
   - 在Pangolin的build目录下sudo make uninstall
   - sudo rm -R /usr/local/include/pangolin
   - 重装v0.5版本的Pangolin
   - 在/include/System.h中加入#include <unistd.h>
   
6. 如需在ROS环境下运行ORB_SLAM2
   - chmod +x build_ros.sh
   - 在~/.bashrc中加入：
   	export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:~/git/ORB_SLAM2/Examples/ROS/
   	再运行./build_ros.sh
   - 报rospkg相关错误：sudo pip3 install rospkg
   - 报boost库相关错误：Examples/ROS/ORB_SLAM2中的CMakeLists.txt的set(LIBS...)末尾加入-lboost_system
   
7. 运行单目示例
   - ./Examples/Monocular/mono_tum Vocabulary/ORBvoc.txt Examples/Monocular/TUM1.yaml Data/rgbd_dataset_freiburg1_desk
   - 即readme中提到的：
   	/Examples/Monocular/mono_tum Vocabulary/ORBvoc.txt Examples/Monocular/TUMX.yaml PATH_TO_SEQUENCE_FOLDER
   - sequence从https://vision.in.tum.de/data/datasets/rgbd-dataset/download中下载
   
8. 运行数据预处理associate
   - 在https://vision.in.tum.de/data/datasets/rgbd-dataset/tools中，选择associate.py；详细地址为https://svncvpr.in.tum.de/cvpr-ros-pkg/trunk/rgbd_benchmark/rgbd_benchmark_tools/src/rgbd_benchmark_tools/associate.py。
   - python2 associate.py rgb.txt depth.txt > associate.txt
   - python2 associate.py associate.txt groundtruth.txt > associate_with_groundtruth.txt
   
9. 变量命名规范（前缀）
   - m	类的成员变量
   - p	指针
   - b	布尔型
   - v	向量
   - t	线程
   - l	列表