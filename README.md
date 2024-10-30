# ros1_noetic_husky_dev_env

A development environment which uses docker, ros1 noetic, and gazebo. Allows for package development and testing for Clearpath husky robot .

This environment loads any packages one directory above the `ros1_noetic_husky_dev_env` directory into the container. This allows for easy development and testing of packages in a consistent environment.
Once the container is running, you can use any normal ROS1 commands to build and run your packages.

Gazebo simulations are also available in this environment, GPUs are currently not supported but can be added by modifying the docker files.

## Setup

Clone this repository to a directory with the package(s) you are developing.

You'll now need to build the docker image. 
If you have any custom packages that you would like to be built into the image, such as custom URDF for your husky model, you can add them to the `custom_packages` directory and they will be built into the image.

From the `ros1_noetic_husky_dev_env` directory, run the following command to build the docker image: `docker compose build`


## Usage

After building the image, you can run the development environment with the following command: `docker-compose run dev_env`

### Tips

If your development requires multiple terminals, you can run `docker-compose run dev_env` multiple times.

The intended project structure is as follows:

```bash
.
├── ros1_noetic_husky_dev_env
│   ├── custom_packages
│   ├── docker-compose.yaml
│   ├── Dockerfile.ros1_noetic_gazebo_husky_dev
│   ├── LICENSE
│   └── README.md
└── some_ros1_pkg
...
```

If you're going to be running a GUI or Gazbeo simulation, you'll need to allow X11 forwarding. On Linux, you can run `xhost +local:root` to allow the container to connect to your X server. 