ROBOT_ID=0

build:
	docker build -f Dockerfile.lidar . -t swarmslam

cpu_run:
	docker run -itd --rm --ipc host --net host --pid host --name swarmslam swarmslam

gpu_run:
	docker run -itd --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" --gpus all -v /dev:/dev -v /home/animesh/cslam_experiments/data/:/Swarm-SLAM/install/cslam_experiments/share/cslam_experiments/data -e NVIDIA_DRIVER_CAPABILITIES=all --rm --ipc host --net host --pid host --name swarmslam swarmslam

agx_run:
	docker run -itd --runtime nvidia --gpus all -v /dev:/dev -e NVIDIA_DRIVER_CAPABILITIES=all --rm --ipc host --net host --pid host --name swarmslam swarmslam

start:
	docker start swarmslam

stop:
	docker stop swarmslam

kill:
	docker kill swarmslam

attach:
	docker exec -it swarmslam bash

swarmslam-lidar:
	docker exec -it swarmslam bash -c "source /opt/ros/humble/setup.bash; source Swarm-SLAM/install/setup.bash; ros2 launch cslam_experiments experiment_lidar.launch.py robot_id:=$(ROBOT_ID)"

swarmslam-graco-lidar:
	docker exec -it swarmslam bash -c "source /opt/ros/humble/setup.bash; source Swarm-SLAM/install/setup.bash; ros2 launch cslam_experiments graco_lidar.launch.py robot_delay_s:=1 launch_delay_s:=1"
	
swarmslam-odom:
	docker exec -it swarmslam bash -c "source /opt/ros/humble/setup.bash; source Swarm-SLAM/install/setup.bash; ros2 launch cslam_experiments rtabmap_ouster_lidar_odometry.launch.py robot_id:=0 scan_cloud_topic:=/warty/lidar_points imu_topic:=/warty/imu/data frame_id:=warty/base_link approx_sync:=true wait_for_transform:=0.0 use_sim_time:=false"
	
swarmslam-odom1:
	docker exec -it swarmslam bash -c "source /opt/ros/humble/setup.bash; source Swarm-SLAM/install/setup.bash; ros2 launch cslam_experiments rtabmap_ouster_lidar_odometry.launch.py robot_id:=0"
