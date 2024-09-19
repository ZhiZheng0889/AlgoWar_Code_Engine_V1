Here’s a step-by-step guide for setting up Ubuntu and Piston in markdown format:

```markdown
# Setting Up Ubuntu and Piston Code Execution Engine

This guide provides the steps for setting up a code execution engine using Piston on Ubuntu.

## Prerequisites

- Docker installed on Ubuntu
- Docker Compose installed

## Step 1: Install Docker

If Docker is not already installed on your Ubuntu system, follow these steps:

1. **Update the apt package index**:
   ```bash
   sudo apt update
   ```

2. **Install required packages**:
   ```bash
   sudo apt install apt-transport-https ca-certificates curl software-properties-common
   ```

3. **Add Docker’s official GPG key**:
   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```

4. **Add the Docker repository to apt sources**:
   ```bash
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

5. **Update the package index again**:
   ```bash
   sudo apt update
   ```

6. **Install Docker**:
   ```bash
   sudo apt install docker-ce
   ```

7. **Verify Docker installation**:
   ```bash
   docker --version
   ```

## Step 2: Install Docker Compose

1. **Download the Docker Compose binary**:
   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```

2. **Apply executable permissions to the binary**:
   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```

3. **Verify Docker Compose installation**:
   ```bash
   docker-compose --version
   ```

## Step 3: Set Up Piston

1. **Clone the Piston repository**:
   ```bash
   git clone https://github.com/engineer-man/piston.git
   ```

2. **Navigate to the Piston directory**:
   ```bash
   cd piston
   ```

3. **Create the Docker container using Docker Compose**:
   ```bash
   docker-compose up -d
   ```

4. **Check that the Piston API is running**:
   ```bash
   docker logs piston_api
   ```

   The log should show the API server started on port `2000`.

## Step 4: Test the API Locally

1. **Test the API endpoint**:
   ```bash
   curl http://localhost:2000
   ```

   You should get a response like:
   ```json
   {"message": "Piston v3.1.1"}
   ```

2. **Run a sample Python script using the Piston API**:
   ```bash
   curl -X POST http://localhost:2000/api/v2/execute -H "Content-Type: application/json" -d '{
     "language": "python3",
     "version": "3.9.4",
     "files": [{
       "name": "main.py",
       "content": "print(\"Hello, world!\")"
     }]
   }'
   ```

   The response should include the output of the code execution:
   ```json
   {
     "language": "python3",
     "version": "3.9.4",
     "run": {
       "stdout": "Hello, world!\n",
       "stderr": "",
       "output": "Hello, world!\n",
       "code": 0,
       "signal": null
     }
   }
   ```

## Step 5: List Available Languages

To see the available runtimes (languages supported by Piston):

```bash
curl http://localhost:2000/api/v2/runtimes
```

This will return a list of all available languages and versions.

## Step 6: Managing Piston

- **Stop Piston API**:
  ```bash
  docker-compose down
  ```

- **Restart the API**:
  ```bash
  docker-compose up -d
  ```

## Optional: Additional Configuration

- If you need to change any configuration, modify the environment variables in the `docker-compose.yml` file or add your own configuration.
- To integrate this engine with a web interface or another service, you can use the `/execute` endpoint to send code execution requests.

## Conclusion

You have successfully set up the Piston code execution engine using Docker on Ubuntu. Now you can use the Piston API to run code snippets in various programming languages.
```

This markdown guide walks through the installation and setup of Piston on Ubuntu, including the necessary tools like Docker and Docker Compose. Let me know if you need further modifications!# AlgoWar_Code_Engine_V1
