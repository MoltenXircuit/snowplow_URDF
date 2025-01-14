# snowplow_URDF
urdf and sick lidar code

Setup:

install Ros 2 Iron, ensure rviz works using
rviz2


Install robot description:

cd $snowplow_ws  #replace with ws directory
(put this folder into the ws directory)

Install sick_scan_xd scripts:

cd $snowplow_ws  #replace with ws directory

pushd src

git clone https://github.com/SICKAG/sick_scan_xd.git

popd

rosdep update && rosdep install --from-paths src --ignore-src -r -y
rm -rf ./build ./devel ./install ./build_isolated ./devel_isolated ./install_isolated ./log
colcon build --symlink-install --cmake-args " -DROS_VERSION=2" " -DCMAKE_ENABLE_EMULATOR=0" "-DCMAKE_BUILD_TYPE=Release" --event-handlers console_direct+
sudo ldconfig

Install extra scripts:

sudo apt-get update

sudo apt install ros-iron-xacro ros-iron-joint-state-publisher-gui


To run:

cd $snowplow_ws  #replace with ws directory

source install/setup.bash

ros2 launch Snowplow_URDF_description display.launch.py

if a change is made to the files, rebuild:

colcon build
