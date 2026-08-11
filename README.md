# ROS2 Jazzy Docker Template
 - A template for ROS2 Jazzy development in a Ubuntu 24.04 (Noble) Docker environment. 

## Compatibility
This Docker environment has only been tested on Ubuntu 24.04 26.04 hosts at this time but likely should work on most Linux hosts. 

This installation process is meant for an Ubuntu host. You likely will have to change certain commands (notably in steps 1-4) to be compatible for your Linux distribution. 

## Usage & Contribution Guidelines 
This codebase has been licensed with an MIT license to allow and promote free and open access to code that is useful for ROS2 development. 

As per the MIT License, all/any part(s) of this codebase may be forked and modified for use. Please read the notes below for guidance. I hope this codebase helps guide you on your programming journey! 

Note: Pull requests that include ROS2 development files will not be accepted. Please ensure your PRs do not add files into /src or add other development folders such as /build, /install, or /log. Files typically should not be added, only modified.

## Installation
1. Update Your OS:

```bash
sudo apt update && sudo apt upgrade -y
```

2. Install Docker Desktop For Linux

https://docs.docker.com/desktop/setup/install/linux/

3. Verify Docker Installed Correctly

```bash
sudo systemctl status docker
sudo docker run hello-world # should output a hello from docker message
```

4. Add yourself to the docker group (so you can run docker commands without sudo)

```bash
sudo usermod -aG docker $USER # (add yourself to docker group)
su - $USER # (refresh group permissions)
id # make sure (docker) is present in this output
docker run hello-world # now you should be able to run docker commands without sudo
```

5. Install VSCode

```bash
sudo snap install code
```

6. Install the below VSCode Extensions. Close VSCode after this step.
- Microsoft C/C++ `ms-vscode.cpptools` (recommended)
- Microsoft Python`ms-python.python` (recommended)
- Microsoft Pylance `ms-python.vscode-pylance` (recommended)
- Robotics Developer Environment `ranch-hand-robotics.rde-pack`  (optional)
- Docker `ms-azuretools.vscode-docker` (**required**)
- Dev Containers `ms-vscode-remote.remote-containers` (**required**)

7. Clone this repository

```bash
git clone git@github.com:[GITHUB_USERNAME]/ros2_jazzy_docker_template.git
```

8. Build the Docker Image

```bash
cd ./ros2_jazzy_docker_template
docker compose up -d --build
```

9. Enter a terminal in the Docker container

```bash
docker compose exec ros2 bash
whoami # this should return "ubuntu" and not your normal username
ros2 # this should return usage information for the ros2 command, indicating ros2 was successfully sourced
```

10. Open VSCode from your workspace (run these commands from host, not inside the docker container)

```bash
cd ./ros2-ws
code .
```

11. Open the workspace in the container

VSCode should popup with a “Reopen in Container” button. If it does, click the button. If it does not, follow the below steps:

- Click Ctrl+Shift+P
- Search for and select `Dev Containers: Reopen in Container`

12. Confirm the workspace is open properly
- Open a new terminal in VSCode and run
```bash
whoami # this should return "ubuntu" and not your normal username
ros2 # this should return usage information for the ros2 command, indicating ros2 was successfully sourced
```
13. Enjoy your new development environment

## Using Git With Your Workspace
The .gitignore in this project is meant to maintain its status as a reproducible template for any ROS2 Jazzy project. This means that it ignores all files and folders unique to a specific project. If you want to use Git to manage your ROS2 projects, add specific ROS2 packages inside of ros2-ws/src and make each package its own repository. This will allow you to use Git and this template repository. 

## Docker Tips
Stop the container
```bash
docker compose stop
```

Start the container
```bash
docker compose start
```

Launch a terminal inside the container
```bash
docker compose exec ros2 bash
```

Exit the terminal's container
```bash
exit
```

Re-build and launch the container
``` bash
docker compose up -d --build
```

## Contributors
- Leo Abubucker (leoabubucker): Repository Owner

## Software License
[MIT](https://choosealicense.com/licenses/mit/)

Copyright (c) 2026 Leo Abubucker

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
