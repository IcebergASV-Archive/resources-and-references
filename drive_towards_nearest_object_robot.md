# drive_towards_nearest_object_robot.md

Example simulation using a 2 wheeled differential drive robot. Detects objects using YOLOv5 and real sense camera, and drives towards nearest objects. 
Following [this](https://www.youtube.com/watch?v=Ob8lGOHBrig) youtube video.

First install ROS navigation stack:
```
$ sudo apt-get install ros-noetic-navigation`
```
Install librealsense packages:
```
$ sudo apt install libssl-dev pkg-config libgtk-3-dev libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev
```

Now git clone RealSense repository:
```
$ giclone https://github.com/IntelRealSense/librealsense
```

Navigate to librealsense directory and create a build directory:

```
$ cd librealsense/
$ mkdir build
$ cd build
```
Execute cmake commands:

```
$ cmake .. -DBUILD_EXAMPLES=true
$ make
$ sudo make install
```

Download [this](https://drive.google.com/file/d/1j0dnmDbLJgjgTReMh3axaEb9ky-G2PvT/view?usp=share_link) zip file. (yolo_nav.zip in the Drive under /January - March/Software). Extract the zip file to the home directory. 

Copy models into Gazebo models directory - need to update. 

```
cd
cd /.gazebo
mkdir models
cd /Downloads/yolo_nav/models
mv hatchback ~/.gazebo/models
mv hatchback_blue ~/.gazebo/models
mv yolo_nav_stage ~/.gazebo/models
mv person_standing ~/.gazebo/models
```


Create a new catkin workspace. Replace 'youruser'. - UPDATE use the exsisting yolo_nav folder. add in more stuff from the video. 

```
cd
mkdir -p ~/yolo_nav_ws/src
cd yolo_nav_ws/
mkdir UI
catkin_make
source devel/setup.bash
echo $ROS_PACKAGE_PATH /home/youruser/yolo_nav_ws/src:/opt/ros/noetic/share
```

install seaborn
install tqdm
install 
sudo apt-get install ros-noetic-effort-controllers



in /home/grace/.local/lib/python3.8/site-packages/torch/nn/modules/upsampling.py

change this:
```
    def forward(self, input: Tensor) -> Tensor:
        return F.interpolate(input, self.size, self.scale_factor, self.mode, self.align_corners)
        #return F.interpolate(input, self.size, self.scale_factor, self.mode, self.align_corners,
                             #recompute_scale_factor=self.recompute_scale_factor)
```


add self.show() to line 72 of controller.py.
