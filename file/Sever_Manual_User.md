# MMIO Server User Manual
> ## Latest Update: 2025-08-06

Here are commands often used when you connect to the server. 

### Reminder
If you encounter any of the following situations, please contact the administrators or leave a message in the lab's Discord:
- You need to use any command starting with sudo
- You need to install software on the server
- You need some technical supports
- You want to add something into todo list
- Something is going wrong
- You find an error in the manual


## Server Status
> ### Supermicro: ✅ Work Normally
> ### R740: ✅ Work Normally


## !!! WARNING !!!
> ### The server could only be accessed by the Lab's IP addresses. 
> ### Always use [VPN client](https://reurl.cc/9nR4Yd) to access the server.
> ### Always use [virtual environments](#virtual-environment-top) for coding.
> ### Always check the [GPU usage](#gpu-resource-top) before you start training.


## Table of Contents
- [Connect to the Server](#connect-to-server-top)
- [Basic Command Line](#basic-command-line-top)
- [File Manipulation](#file-manipulation-top)
- [Virtual Environment](#virtual-environment-top)
- [GPU Resource](#gpu-resource-top)
- [User-Specific CUDA](#user-specific-cuda-top)
- [Git & GitHub](#git--github-top)
- [tmux](#tmux-top)
- [Todo](#todo-todo)


## Connect to Server <a href="#mmio-server-user-manual" style="float:right;">Top</a>

**There's a information sheet behind the door of YL430 & YL432.**

### CLI version

```
ssh <username>@<server_IP> -p <port>
```
- `<server_IP>` IP address of the remote server
- `-p <port>` Specify the SSH port of remote server
    - Default: `22`

### GUI version

You can also use the SSH service via visualized software. 
- MobaXTerm ([Installer](https://reurl.cc/7VMMvd))


## Basic Command Line <a href="#mmio-server-user-manual" style="float:right;">Top</a>

List files and subdirectories inside the current directory
```
ls 
```

---

List files and subdirectories inside `<dir>`
```
ls <dir>
```

---

Change directory to `<dir>`
```
cd <dir>
```

---

Show absolute path of current directory
```
pwd
```

---

Change directory to parent directory
```
cd ..
```

---

Change directory to home directory
```
cd ~
```

---

Execute python file
```
python <file>.py
```

### Text editor

You can use a text editor like **nano** or **vim** to edit files. **nano** is more user-friendly for beginners.

```
nano <filepath>
```

or

```
vim <filepath>
```


## File Manipulation <a href="#mmio-server-user-manual" style="float:right;">Top</a>

### Basic operation

Copy a file or directory
```
cp <source> <destination>
```

---

Move a file or directory
```
mv <source> <destination>
```

---

Delete file or empty directory
```
rm <file>
```

---

Delete non-empty directory
```
rm -rf <file>
```
- `-r` Delete all subfolders
- `-f` Force mode

---

Delete empty directory
```
rmdir <file>
```

---

Create a new directory
```
mkdir <directory>
```

---

Modify file permissions
```
chmod <username>:<usergroup>:others <dir>
```
- `r` Read (4), `w` Write (2), `x` Execute (1)
- `777` rwxrwxrwx: All users can read, write, and execute
- `700` rwx------: Only `<username>` can read, write, and execute
- `550` r-xr-x---: Only `<username>` and users in `<usergroup>` can read and execute

### Bash script

Create script
```
nano <file>.sh
```

---

Make script executable
```
chmod +x <file>.sh
```

---

Execute script
```
./<file>.sh
```

### Auto-Start program when login

```
nano ~/.bashrc
```


## Virtual Environment <a href="#mmio-server-user-manual" style="float:right;">Top</a>

### Basic operation

Check conda version
```
conda --version
```

---

Create a new environment
```
conda create -n <env> python=3.X
```
- `-n` Specify the name of virtual environment

---

Activate / Deactivate the environment
```
conda activate|deactivate <env>
```

---

Remove the environment
```
conda remove -n <env> --all
```
- `--all` Remove the entire environment

or 

```
conda env remove -n <env>
```

---

Check all environments in your account (`<env>` with star sign is current environment)
```
conda info -e
```
- `-e` Show environment information

or

```
conda env list
```

### Install package

Install latest version
```
pip install <package>
```

or

```
conda install <package>
```

---

Install specific version
```
pip install <package>=X.XX.X
```

or

```
conda install <package>=X.XX.X
```


## GPU Resource <a href="#mmio-server-user-manual" style="float:right;">Top</a>

### Server GPU

Server        | GPU          | Manufacturer    | Quantity    | Memory    |
--------------|--------------|-----------------|-------------|-----------|
Supermicro    | A100         | Nvidia          | 2           | 80GB      |
Supermicro    | RTX A6000    | Nvidia          | 2           | 48GB      |
R740          | A40          | Nvidia          | 1           | 48GB      |

### Usage information

Static display
```
nvidia-smi
```

or 

Dynamic display
```
nvitop
```


## User-Specific CUDA <a href="#mmio-server-user-manual" style="float:right;">Top</a>

Some programs may need to apply on a specific CUDA version. You can install CUDA locally in your home directory without needing root access. 

**Note that the default CUDA version in both servers are `CUDA 11.8`.**

### Install Procedure (Example: cuda-12.2)

Download the [installer](https://developer.nvidia.com/cuda-toolkit-archive) from the CUDA Toolkit Archive:
```
wget https://developer.download.nvidia.com/compute/cuda/12.2.0/local_installers/cuda_12.2.0_535.54.03_linux.run
```
- Web page selection: *Linux* >> *x86_64* >> *Ubuntu* >> *20.04* >> *runfile (local)*

---

Make the installer executable
```
chmod +x cuda_12.2.0_535.54.03_linux.run
```

---

Run the installer
```
./cuda_12.2.0_535.54.03_linux.run --silent --toolkit --toolkitpath=$HOME/cuda-12.2
```
- `--silent` Silent mode
- `--toolkie` Only install toolkit
- `--toolkitpath` Specify installation path
- `$HOME` Home directory

---

Append system path to `bashrc`
```
nano ~/.bashrc
```
- `~/.bashrc`

   ```
   export PATH=$HOME/cuda-12.2/bin:$PATH
   export LD_LIBRARY_PATH=$HOME/cuda-12.2/lib64:$LD_LIBRARY_PATH
   ```

---

Reload shell
```
source ~/.bashrc
```

---

Verify CUDA version:

   ```
   nvcc --version
   ```

### Reminder
- This installation only contains the CUDA toolkit (not the driver).
- You can install multiple versions by changing the target folder.
- Switching between versions can be done by updating `PATH` and `LD_LIBRARY_PATH`.
- You can switch to the system-default version by deleting the commands added in `~/.bashrc`


## Git & GitHub <a href="#mmio-server-user-manual" style="float:right;">Top</a>

### Initialize code space

Clone repository
```
git clone https://github.com/<username>/<project>.git
```

---

Change to repository directory
```
cd <project>
```

---

Pull the code from remote repository
```
git pull
```

### Synchronize code space 

Add Modification to staging area
```
git add .
```

---

Commit
```
git commit -m "<commit message>"
```

---

Push the code to remote repository
```
git push
```


## tmux <a href="#mmio-server-user-manual" style="float:right;">Top</a>

tmux is a terminal multiplexer that lets you run and manage multiple terminal sessions in one window. It supports session persistence (even after disconnecting SSH), window splitting, and is great for remote work.

For more detail, please check the onlin [tutorial](https://blog.gtwang.org/linux/linux-tmux-terminal-multiplexer-tutorial/)

### Basic Operation

Open tmux session
```
tmux
```

---

List all of sessions
```
tmux ls
```

---

Restore to specific session
```
tmux a -t <session>
```
- `a` Attach
- `-t <session>` Specify session number

---

End current session
```
logout
```

---

End other session
```
tmux kill-session -t <session>
```


## Todo <a href="#mmio-server-user-manual" style="float:right;">Top</a>

- FSL
- VS Code Setup


<!-- ## FSL

### Undone

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
![alt text](https://github.com/MuajiiTsai/MMIO_Ubuntu/blob/main/img/fsl.png) -->