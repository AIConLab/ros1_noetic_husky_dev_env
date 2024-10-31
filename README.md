# ros1_noetic_husky_dev_env

A development environment which uses docker, ros1 noetic, and gazebo. Allows for package development and testing for Clearpath husky robot .

This environment loads any packages one directory above the `ros1_noetic_husky_dev_env` directory into the container. This allows for easy development and testing of packages in a consistent environment.
Once the container is running, you can use any normal ROS1 commands to build and run your packages.

Gazebo simulations are also available in this environment, GPUs are currently not supported but can be added by modifying the docker files.

## Setup

Clone this repository to a directory with the package(s) you are developing.
In the directory with the packages, create a directory called `some_name_ws` where `some_name` is the name of your workspace.

## Usage

After building the image, you can run the development environment with the following command: `docker-compose run dev_env`

### Tips

If your development requires multiple terminals, you can run `docker-compose run dev_env` multiple times.

The intended project structure is as follows:

```bash
.
├── husky_dev_ws
├── ros1_noetic_husky_dev_env
│   ├── docker-compose.yaml
│   ├── Dockerfile.ros1_noetic_gazebo_husky_dev
│   ├── LICENSE
│   └── README.md
└── src
    ├── some_ros1_pkg
    └── utsan06_husky
...

```

To have a persistent workspace you can mount the workspace directory to the container. This can be done by adding the following line to the `docker-compose.yaml` file:

```yaml
volumes:
  - ../some_ws:/root/some_ws
  - ../src/:/root/some_ws/src/extern_pkgs

```

If you're going to be running a GUI or Gazbeo simulation, you'll need to allow X11 forwarding. On Linux, you can run `xhost +local:root` to allow the container to connect to your X server. 