# Install Hummingbot with Docker

CoinAlpha publishes [Docker images](https://hub.docker.com/r/coinalpha/hummingbot) for the `latest` and `development` builds of Hummingbot, as well as every version. 

You can install Docker and Hummingbot by selecting the following options below:

- **Scripts**: download and use automated install scripts
- **Manual**: run install commands manually

## Linux/Ubuntu

_Supported versions: 16.04 LTS, 18.04 LTS, 19.04_

### Install Docker

=== "Scripts"

    ```bash
    # 1) Download Docker install script
    wget https://raw.githubusercontent.com/hummingbot/hummingbot/master/installation/install-docker/install-docker-ubuntu.sh

    # 2) Enable script permissions
    chmod a+x install-docker-ubuntu.sh

    # 3) Run installation
    ./install-docker-ubuntu.sh
    ```

=== "Manual"

    ```bash
    # 1) Update Ubuntu's database of software
    sudo apt-get update

    # 2) Install tmux
    sudo apt-get install -y tmux

    # 3) Install Docker
    sudo apt install -y docker.io

    # 4) Start and Automate Docker
    sudo systemctl start docker && sudo systemctl enable docker

    # 5) Change permissions for docker (optional)
    # Allow docker commands without requiring sudo prefix
    sudo usermod -a -G docker $USER

    # 6) Close terminal
    exit
    ```

!!! warning
    Please restart terminal — close and restart your terminal window to enable the correct permissions for `docker` command before proceeding to next step.

### Install Hummingbot

=== "Scripts"

    ```bash
    # 1) Download Hummingbot install, start, and update script
    wget https://raw.githubusercontent.com/hummingbot/hummingbot/master/installation/docker-commands/create.sh
    wget https://raw.githubusercontent.com/hummingbot/hummingbot/master/installation/docker-commands/start.sh
    wget https://raw.githubusercontent.com/hummingbot/hummingbot/master/installation/docker-commands/update.sh

    # 2) Enable script permissions
    chmod a+x *.sh

    # 3) Create a hummingbot instance
    ./create.sh
    ```

=== "Manual"

    ```bash
    # 1) Create folder for your new instance
    mkdir hummingbot_files

    # 2) Create folders for logs, config files and database file
    mkdir hummingbot_files/hummingbot_conf
    mkdir hummingbot_files/hummingbot_logs
    mkdir hummingbot_files/hummingbot_data
    mkdir hummingbot_files/hummingbot_scripts

    # 3) Launch a new instance of hummingbot
    docker run -it \
    --network host \
    --name hummingbot-instance \
    --mount "type=bind,source=$(pwd)/hummingbot_files/hummingbot_conf,destination=/conf/" \
    --mount "type=bind,source=$(pwd)/hummingbot_files/hummingbot_logs,destination=/logs/" \
    --mount "type=bind,source=$(pwd)/hummingbot_files/hummingbot_data,destination=/data/" \
    --mount "type=bind,source=$(pwd)/hummingbot_files/hummingbot_scripts,destination=/scripts/" \
    coinalpha/hummingbot:latest
    ```

## MacOS

You can install Docker by [downloading an installer](https://docs.docker.com/docker-for-mac/install/) from the official page. After you have downloaded and installed Docker, restart your system if necessary.

=== "Scripts"

    ```bash
    # 1) Download Hummingbot install, start, and update script
    curl https://raw.githubusercontent.com/hummingbot/hummingbot/master/installation/docker-commands/create.sh -o create.sh
    curl https://raw.githubusercontent.com/hummingbot/hummingbot/master/installation/docker-commands/start.sh -o start.sh
    curl https://raw.githubusercontent.com/hummingbot/hummingbot/master/installation/docker-commands/update.sh -o update.sh

    # 2) Enable script permissions
    chmod a+x *.sh

    # 3) Create a hummingbot instance
    ./create.sh
    ```

=== "Manual"

    ```bash
    # 1) Create a folder for your new instance
    mkdir hummingbot_files

    # 2) Create folders for logs, config files and database file
    mkdir hummingbot_files/hummingbot_conf
    mkdir hummingbot_files/hummingbot_logs
    mkdir hummingbot_files/hummingbot_data
    mkdir hummingbot_files/hummingbot_scripts

    # 3) Launch a new instance of hummingbot
    docker run -it \
    --network host \
    --name hummingbot-instance \
    --mount "type=bind,source=$(pwd)/hummingbot_files/hummingbot_conf,destination=/conf/" \
    --mount "type=bind,source=$(pwd)/hummingbot_files/hummingbot_logs,destination=/logs/" \
    --mount "type=bind,source=$(pwd)/hummingbot_files/hummingbot_data,destination=/data/" \
    --mount "type=bind,source=$(pwd)/hummingbot_files/hummingbot_scripts,destination=/scripts/" \
    coinalpha/hummingbot:latest
    ```

## Windows

The Hummingbot codebase is designed and optimized for UNIX-based systems such as macOS and Linux. For Windows users, we recommend running Hummingbot in **Windows Subsystem for Linux (WSL)**.

WSL lets developers run a Linux environment directly on Windows, unmodified, without the overhead of a traditional virtual machine or dualboot setup. With WSL, Windows 10/11 users are able to run a Linux Virtual Machine without performance loss, and without the need of dual boot. See [here](https://docs.microsoft.com/en-us/windows/wsl/about) for more detail about WSL.

### Install WSL

**1. Open Powershell as `admin`**

Search for "Powershell" on the start menu, right-click and "run as admin"

![Powershell start](/assets/img/wsl-powershell.png)

**2. Run the Install WSL commmand**

```bash
wsl --install
```

By default, WSL uses the Ubuntu distribution of Linux, which is compatible for Hummingbot.

**3. Start WSL**

After the installation, just type `wsl` on the Powershell or on the Command prompt.

Note that the first time WSL is executed, you will be asked to create a new default username/password.

**4. Install Ubuntu from Windows Store**

Alternatively, after WSL is installed, search for **Ubuntu** in the Windows Store and install it as an app in the Start menu. That way, you don't have to run Powershell every time you use Hummingbot. 

![Powershell start](/assets/img/wsl-distros.png)

**5. Install Docker and Hummingbot**

With WSL installed, you now have a Linux Virtual Machine running under Windows.

![Linux on Windows](/assets/img/wsl-running.png)

Follow the instructions in the **Install Hummingbot** section above to complete the installation process.
