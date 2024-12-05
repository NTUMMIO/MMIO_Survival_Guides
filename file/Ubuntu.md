MMIO_Ubuntu
===
**Here are commands often used when you connect to the server.**  
**If you have to use any command starting with "_sudo_", please ask sudoers (admins) for help.**

## Command line for begginers
```
ls  //list files and subdirectorys inside the current directory
cd {path}  //change directory to {path}
cd ..  //change directory to the parent directory
mkdir {name}  //create a new directory
```

## Connect to the Server
Entering the following command in your terminal:
```
ssh <username>@<Server_IP> -p <port>
```
*Server_IP* : ip address of the remote server.  
You can also use SSH service via visualized softwares. (MobaXTerm, FileZilla, etc.)  
If the output responds with **"Command not found"**, please contact the admins for installing OpenSSH Client.  
### Change password
```
$ passwd
```
### Check Linux Disk Space
```
df
```

## Virtual Environment - Miniconda
#### Check conda version
```
conda --version
conda -V
```
#### Create a new environment
```
conda create -n {envName} python=3.x  //specify the python version
```
#### Activate/Deactivate the environment
```
conda activate {envName}
conda deactivate {envName}
```
#### Remove the environment
```
conda remove -n {envName} --all
```
#### Check all environments in your account
```
conda info -e
conda env list
```
#### Install a package to the activated env
```
conda install {packageName}  //latest version
conda install {packageName}=1.0.0  //specific version
pip install {packageName}  //you can also use pip rather than conda
```
or google the official guide of installing the package.


## FSL
Add the following code into .profile:
```
FSLDIR=/usr/local/fsl
. ${FSLDIR}/etc/fslconf/fsl.sh
PATH=${FSLDIR}/bin:${PATH}
export FSLDIR PATH
```
then, **close SSH connection and reconnect to the server.**
#### To open FSL:
```
fsl
```
![alt text](https://github.com/MuajiiTsai/MMIO_Ubuntu/blob/main/img/fsl.png)

## tmux
Reference: https://blog.gtwang.org/linux/linux-tmux-terminal-multiplexer-tutorial/

<!-- # SSH Settings

## For Sudoers
### Add user
#### 1. 
```
sudo adduser <username>
```
or
```
sudo adduser <username> sudo
```
When adding a new user as sudoer.
#### 2. Change the permission (drwx------)
```
sudo chmod 700 /home/<username>
```
#### 3. Check users' disk usage (du)
```
sudo du -sh /home/*
``` -->

<!-- ## Server
To check whether SSH is available on the remote server, run:
```
ssh localhost
```
If the output responds with "Connection refused", move on to **installing SSH on the server**.
#### 1. Run the following command to install the SSH server
```
sudo apt-get install openssh-server ii
```
#### 2. Run “ssh localhost” to check if the installation is completed. Enter yes or y to continue.
#### 3. To check the status of the service, enter:
```
sudo service ssh status
```
#### 4. The output should respond that the service is active. You will need to enable it when the service is down by running the command:
```
systemctl start sshd
```

## Client
To check whether you have the SSH client on your system, run the command:
```
ssh
```
If the output responds with "Command not found", move on to installing OpenSSH Client.
#### Run the following command to install the SSH client:
```
sudo apt install openssh-client
```

## Cuda
https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#removing-cuda-toolkit-and-driver  

#### Cuda uninstall
To remove CUDA Toolkit:  
```
sudo apt-get --purge remove "cuda*" "*cublas*" "*cufft*" "*cufile*" "*curand*" \
 "*cusolver*" "*cusparse*" "*gds-tools*" "*npp*" "*nvjpeg*" "nsight*" "*nvvm*"
```
To remove NVIDIA Drivers:  
```
sudo apt-get --purge remove "*nvidia*" "libxnvctrl*"
```
To clean up the uninstall:  
```
sudo apt-get autoremove
``` -->

