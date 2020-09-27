程序说明：
1 基于已知地图map（该map可基于map_server包导入）下的避障，需要加入amcl（其提供map-odom间的坐标变换）
前提条件：
1）进行velodyne的有线连接（注意：有的时候启动velodyne的时候需要进行端网，联网条件下启动时需进行相关配置）
2）基于公头转usb线进行autolabor小车与工控机间的连接
赋予小车驱动程序串口权限sudo chmod 777 /dev/ttyUSB0 ，此时便可基于键盘控制小车运动了，小车订阅的话题是cmd_vel
启动小车避障程序
cd lc
catkin_make
source devel/setup.bash
roslaunch test1 navigation1.launch
2 直接基于小车驱动autolabor，velodyne与move_base包进行避障，简称无图下的避障，去除了map与amcl，从官网move_base介绍中可以发现，其属于可选项

