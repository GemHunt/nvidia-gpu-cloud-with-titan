# nvidia-gpu-cloud-with-titannvidia-gpu-cloud-with-titan

This is my notes after third installs.

Once the server is set up the promise of a 5 minute install holds true, but you still need to know the basics of using Docker. 

**Ubunutu Setup:**
* Following with:
* http://docs.nvidia.com/ngc/ngc-titan-setup-guide/index.html
* Burn 16.04.3 Desktop AMD64 Aug 2017 ISO to DVD
* (They really should state the exact ISO to pull.) 
* https://download.docker.com/linux/ubuntu/dists/xenial/pool/stable/amd64/
* Don’t check the boxes for “download updates or install third party software”
* Force UEFI Installation:click “Go Back” 
* “Erase Disk and install Ubuntu”: Install Now
* On first start up make sure 4.10 kernel is running by typing:
* uname -a
* Follow the directions at:
* http://docs.nvidia.com/ngc/ngc-titan-setup-guide/index.html
* Make script files by copying out of Firefox(Chrome copies wrong)

* I keeping having to run second script more than once. If so:
* Remove reboot at end to make sure the second script works
* You might have to run manually:
* sudo rm /etc/apt/sources.list.d/cuda.list
* sudo apt-key add /var/nvidia-driver-local-repo-387.34/7fa2af80.pub
* Then run the second script again, then reboot. 

**Using Nvidia GPU Cloud with Titan Usage:**
* cd /
* mkdir digits-jobs
* mkdir data
* There is an issue that I have to use sudo and I have to manually start the daemon
* start the docker Daemon: 
* sudo dockerd
* docker login -u '$oauthtoken' --password-stdin nvcr.io <<< 'Qt4M2VkL---------Your API KEY -------3ZGZZmNIw'
* docker pull nvcr.io/nvidia/digits:18.01
* nvidia-docker run -it --rm --net=host --name digits -v /data:/data -v /digits-jobs:/workspace/jobs nvcr.io/nvidia/digits:18.01
* In a new terminal open a shell inside the workspace:
* docker exec -it digits /bin/bash
* To show the base directory for the frameworks inside the container:
* cd /opt/ | ls
* To show the binaries the container has:
* cd/usr/local/bin

***********************************************************************************
**Docker tasks for myself**
* Write a script to start a container on system startup
* Fix the permissions issue 

**Docker notes for myself:**
* https://ngc.nvidia.com
* http://docs.nvidia.com/ngc/ngc-user-guide/index.html
* https://github.com/NVIDIA/nvidia-docker/wiki/
* https://hub.docker.com/r/nvidia/
* https://github.com/NVIDIA/nvidia-docker/wiki/Third-party
* Why does nvidia sometimes say nvidia-docker or just docker:
* nvidia-docker only modifies the behavior of the run and create Docker commands
* http://phase2.github.io/devtools/common-tasks/ssh-into-a-container/

**Docker commands**
* start the docker Daemon: sudo dockerd
* List containers:
* sudo docker ps
* Shell into container:
* sudo docker exec -it digits /bin/bash
* Use the ID from “docker ps” or name the container when you run it.
