程序说明：
1 有图避障：基于已知地图map（该map可基于map_server包导入）下的避障，需要加入amcl（其提供map-odom间的坐标变换）
前提条件：
1）进行velodyne的有线连接（注意：有的时候启动velodyne的时候需要进行端网，联网条件下启动时需进行相关配置）
2）基于公头转usb线进行autolabor小车与工控机间的连接
赋予小车驱动程序串口权限sudo chmod 777 /dev/ttyUSB0 ，此时便可基于键盘控制小车运动了，小车订阅的话题是cmd_vel
3）其对应导入的move_base中的参数为test包中的param
4) 启动小车避障程序
cd lc
catkin_make
source devel/setup.bash
roslaunch test1 navigation1.launch
5) 启动后rviz界面修改
fixed frame: map

2 无图避障：直接基于小车驱动autolabor，velodyne与move_base包进行避障，简称无图下的避障，去除了map与amcl，从官网move_base介绍中可以发现，其属于可选项
1)其对应导入的move_base中的参数为test包中的param_no_map,后期发现修改该参数后，2D nav goal不起作用，因此还是基于参数config作为无图的配置
roslaunch test1 navigation11.launch
2) 启动后rviz界面修改
fixed frame: odom


3 关键程序说明
（1）局部代价地图的膨胀半径inflation_radius: 0.30 一定要小于全局膨胀半径 inflation_radius: 0.80才行。全局cost map中的障碍物膨胀半径如果比较大，那么全局规划的路径就不会特别逼近墙壁等固态障碍物
（2）代价地图的scan层1线与16线的选择
1）1线
scan:
    topic: scan  #/velodyne_points  #scan   
    data_type: LaserScan   #PointCloud2 # LaserScan
    2）16线
    scan:
    topic: velodyne_points  #scan
    data_type: PointCloud2 # LaserScan
