
# Piston Setup on Ubuntu

This guide provides instructions on how to set up Ubuntu and Piston, a code execution engine, using Docker. Follow the steps below to install dependencies, configure Docker, and run Piston.

## Prerequisites

Before starting, ensure you have the following:

- Ubuntu installed (either as your primary OS, in a virtual machine, or via WSL2 on Windows)
- Admin/root access
- Basic knowledge of using the terminal

## 1. Setting Up Ubuntu

If you're using Windows, you can use Windows Subsystem for Linux (WSL2). Here's how to set it up:

1. **Install WSL2**:
   - Open PowerShell as an administrator and run:
     ```bash
     wsl --install
     ```
   - Reboot your machine if necessary.

2. **Install Ubuntu**:
   - After WSL2 is set up, install Ubuntu from the Microsoft Store or via:
     ```bash
     wsl --install -d Ubuntu
     ```
   - Open Ubuntu and create your user account.

3. **Update Ubuntu Packages**:
   - Open your Ubuntu terminal and run the following to update and upgrade packages:
     ```bash
     sudo apt update && sudo apt upgrade -y
     ```

## 2. Installing Docker and Docker Compose

### 2.1. Install Docker

1. **Install Docker**:
   - Run the following commands to install Docker:
     ```bash
     sudo apt-get update
     sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
     curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
     sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
     sudo apt-get update
     sudo apt-get install docker-ce
     ```

2. **Start Docker**:
   - Ensure Docker is running by starting the service:
     ```bash
     sudo systemctl start docker
     sudo systemctl enable docker
     ```

3. **Check Docker Version**:
   - Confirm Docker is installed by checking the version:
     ```bash
     docker --version
     ```

### 2.2. Install Docker Compose

1. **Install Docker Compose**:
   - Run the following commands to install Docker Compose:
     ```bash
     sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
     sudo chmod +x /usr/local/bin/docker-compose
     ```

2. **Check Docker Compose Version**:
   - Verify Docker Compose is installed by running:
     ```bash
     docker-compose --version
     ```

## 3. Cloning the Piston Repository

1. **Clone the Piston Repo**:
   - Clone the Piston repository from GitHub:
     ```bash
     git clone https://github.com/engineer-man/piston.git ~/piston_project
     ```

2. **Navigate to the Project Directory**:
   - Change into the project directory:
     ```bash
     cd ~/piston_project
     ```

## 4. Configuring and Running Piston

### 4.1. Set Up the Project

1. **Install Dependencies**:
   - If you're working in the `cli` folder, navigate to it and install dependencies:
     ```bash
     cd ~/piston_project/cli
     npm install
     ```

2. **Run Piston with Docker Compose**:
   - Run the following command to build and start the Piston API server:
     ```bash
     docker-compose up --build
     ```

### 4.2. Handling Common Docker Issues

- **Permission Errors**:
  If you encounter permission errors when trying to move or modify files, use the following command to change ownership:
  ```bash
  sudo chown -R $USER:$USER ~/piston_project
  ```

- **Conflicting Containers**:
  If Docker shows an error about a conflicting container name, you can remove the old container:
  ```bash
  docker ps -a  # List all containers
  docker rm <container_id>  # Remove the conflicting container
  ```

  Then run Docker Compose again:
  ```bash
  docker-compose up --build
  ```

## 5. Running Python Code Using Piston

1. **Create a Test Python Script**:
   - Create a simple Python script named `test.py`:
     ```bash
     echo 'print("Hello world!")' > test.py
     ```

2. **Run the Python Script**:
   - Run the script using Piston:
     ```bash
     node index.js run python test.py
     ```

3. **Check API Status**:
   - If you need to check if the Piston API is running, use:
     ```bash
     curl http://localhost:2000
     ```

## 6. Stopping and Restarting Piston

- **Stop Piston**:
  ```bash
  docker-compose down
  ```

- **Restart Piston**:
  ```bash
  docker-compose up --build
  ```

## Conclusion

You now have Piston set up and running on Ubuntu! If you encounter any issues or need further assistance, feel free to explore the [Piston GitHub Repository](https://github.com/engineer-man/piston) for more information and troubleshooting.
```

This `README.md` file includes all necessary steps to set up Ubuntu, Docker, Docker Compose, and Piston, as well as solutions for common issues. Let me know if you'd like any further modifications or adjustments!
