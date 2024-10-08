# MonitorFlow Agent

### Description

This agent is used by the application [monitorflow](https://github.com/Kidoly/monitorflow) to monitor multiple servers/computer. It need to be installed on each server.

### Requirements

- Rust (latest stable version recommended)
- xcb

##### For Debian/Ubuntu-based distributions:

```sh
sudo apt-get update
sudo apt-get install libxcb1-dev
```

##### For Fedora, CentOS, RHEL:

```sh
sudo dnf install libxcb-devel  # Use dnf on Fedora
# or
sudo yum install libxcb-devel  # Use yum on CentOS/RHEL
```

##### For Arch:

```sh
sudo pacman -S libxcb
```

### Installation

#### Step 1: Clone the Repository

```sh
git clone https://github.com/Kidoly/monitorflowagent.git
cd monitorflowagent
```

#### Step 2: Build the Program

```sh
cargo build --release
```

This command compiles your program in release mode. The compiled binary will be located at 'target/release/monitorflowagent'.

#### Step 3: Configuration

You should modify the .env to your own API_KEY and API_URL.

```
API_KEY=your_secret_api_key_here
API_URL=http://localhost:3000/api/api_receive

INTERVAL=600 # Time in seconds between each execution

DISPLAY=:0
RUST_BACKTRACE=1
```

#### Step 4: Running the Program

To run the program, navigate to the directory and execute it:

```sh
cargo run
```

### Setting Up Automatic Launch

#### Linux (Using systemd)

1. Create a systemd service file for your program at '/etc/systemd/system/monitorflowagent.service'. Replace monitorflowagent and /path/to/ with the actual path to your program:

```
[Unit]
Description=MonitorFlow Agent Service

[Service]
ExecStart=/path/to/monitorflowagent
WorkingDirectory=/path/to/your/program/directory
EnvironmentFile=/path/to/your/program/directory/.env
User=youruser
Group=yourusergroup
Restart=always

[Install]
WantedBy=multi-user.target
```

For example if you put the program in your home it should look like this:

```
[Unit]
Description=MonitorFlow Agent Service

[Service]
ExecStart=/home/kidoly/monitorflowagent/target/release/monitorflowagent
WorkingDirectory=/home/kidoly/monitorflowagent
EnvironmentFile=/home/kidoly/monitorflowagent/.env
User=kidoly
Group=kidoly
Restart=always

[Install]
WantedBy=multi-user.target
```

2. Enable and start the service:

```sh
sudo systemctl enable monitorflowagent.service
sudo systemctl start monitorflowagent.service
```

This will set monitorflowagent to start automatically at boot.
