# ROS-based-simulation-tutorial

### 2024.11.22 -- by nyf 显卡问题
- 运行gazebo时，画面偏暗且几乎没有光影效果，外接双显示屏后使用clash-verge非常卡顿，使用`top`发现cpu资源占用很高，估计是显卡问题
- 经检查显卡驱动以及安装并识别，已知gazebo使用OpenGL渲染，使用`glxinfo | grep "OpenGL"`检查发现是英特尔的核显在工作，使用`prime-select query`命令发现输出on-demand，说明系统此时模式是自适应，即低功耗用核显，高功耗用独显，而由于判定问题某些需求大的情况仍被判定为低功耗，故直接使用`nvidia-settings`，进入PRIME Profiles将使用的显卡直接设置为Nidia即可，此时使用prime-select query发现输出就算nvidia了
- 此时在进入gazebo发现环境变明亮了，光影也有了，也不卡顿了，使用`top`发现cpu资源占用也明显降低了