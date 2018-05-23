# nvidia-gpu-cloud-with-titannvidia-gpu-cloud-with-titan

This is my notes after 6-7 installs.

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
* you might have to edit grub to get 4.10 kernel to boot:
*      sudo gedit /etc/default/grub
*       sudo update-grub

* Follow the directions at:
* http://docs.nvidia.com/ngc/ngc-titan-setup-guide/index.html
* Make script files by copying out of Firefox(Chrome copies wrong)

* I keeping having to run second script more than once. If so:
* Remove reboot at end to make sure the second script works
* You might have to run manually:
* sudo rm /etc/apt/sources.list.d/cuda.list
* sudo apt-key add /var/nvidia-driver-local-repo-387.34/7fa2af80.pub
* Then run the second script again, then reboot. 
* Run the 3rd and forth scripts. 

***********************************************************************************
**Software to install on local machines:**
* sudo apt-get install libxss1 libappindicator1 libindicator7
* wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
* sudo dpkg -i google-chrome*.deb
* sudo apt-get install openssh-server
* sudo apt-get install terminator
* download PyCharm Community to ~/pycharm
  https://www.jetbrains.com/pycharm/download/download-thanks.html?platform=linux&code=PCC
* samba:
  https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!
* sudo apt-get install vnc4server
* Setup Desktop Sharing:
* * Search for “Desktop Sharing”:
* * Change the settings
* * Yes: “Allow other users to take control”
* * No: Confirm each access
* * Yes: Set Password
* * No: Automatically Configure ports

**Using Nvidia GPU Cloud with Titan Usage:**
* sudo mkdir /workspace
* cd /workspace
* sudo mkdir jobs
* cd jobs
* login(you need to paste in your key): 
* docker login -u '$oauthtoken' --password-stdin nvcr.io <<< 'Qt4M2VkL---------Your API KEY -------3ZGZZmNIw'
* docker pull nvcr.io/nvidia/digits:18.04
* nvidia-docker run -it --rm --net=host --name digits -v /data:/data -v /digits-jobs:/workspace/jobs nvcr.io/nvidia/digits:18.04
* In a new terminal open a shell inside the workspace:
* docker exec -it digits /bin/bash
* The base directory for the frameworks(caffe/tensorflow/digits/etc) inside the container:
* cd /opt/ | ls
* To show the binaries the container has:
* cd/usr/local/bin

**Other setup :**
* Git clone required git repos
* Move common shell scripts to: /~ and /workspace/jobs/
***********************************************************************************
**Docker tasks for myself**
* Write a script to start a container on system startup

**Links for myself:**
* https://ngc.nvidia.com
* http://docs.nvidia.com/ngc/ngc-user-guide/index.html
* https://github.com/NVIDIA/nvidia-docker/wiki/
* https://hub.docker.com/r/nvidia/
* https://github.com/NVIDIA/nvidia-docker/wiki/Third-party

**Useful Docker commands**
* start the docker Daemon: sudo dockerd
* List containers:
* sudo docker ps
* Shell into container:
* sudo docker exec -it digits /bin/bash
* Use the ID from “docker ps” or name the container when you run it.
