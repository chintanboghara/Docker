# Installing Docker

To install Docker on your machine, follow the instructions based on your operating system. Docker is available for various platforms, including **Linux**, **Windows**, and **macOS**. Below are the steps for each platform:

---

### 1. **Installing Docker on Linux (Ubuntu)**

1. **Update Your Package Index**  
   Run the following command to ensure your package index is up to date:
   ```bash
   sudo apt update
   ```

2. **Install Prerequisite Packages**  
   Install packages that allow `apt` to use a repository over HTTPS:
   ```bash
   sudo apt install apt-transport-https ca-certificates curl software-properties-common
   ```

3. **Add Docker’s Official GPG Key**  
   Add Docker’s official GPG key to your system:
   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   ```

4. **Set Up the Stable Docker Repository**  
   Add the Docker repository to `apt` sources:
   ```bash
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   ```

5. **Install Docker CE (Community Edition)**  
   Update your package index again and install Docker:
   ```bash
   sudo apt update
   sudo apt install docker-ce
   ```

6. **Start and Enable Docker**  
   Enable Docker to start automatically when your system boots:
   ```bash
   sudo systemctl enable docker
   sudo systemctl start docker
   ```

7. **Verify the Installation**  
   Check the installed Docker version:
   ```bash
   docker --version
   ```

8. **(Optional) Run Docker Without `sudo`**  
   By default, Docker requires `sudo` privileges. If you want to run Docker as a non-root user:
   ```bash
   sudo usermod -aG docker $USER
   ```

   After running this command, log out and log back in, or restart your system.

---

### 2. **Installing Docker on macOS**

1. **Download Docker Desktop for Mac**  
   Go to Docker’s official download page:  
   [Download Docker Desktop for Mac](https://www.docker.com/products/docker-desktop)

2. **Install Docker Desktop**  
   Once the `.dmg` file is downloaded, open it and drag the Docker icon to your Applications folder.

3. **Launch Docker**  
   After installation, open Docker from the Applications folder. You may be prompted to grant Docker permissions.

4. **Verify Docker Installation**  
   Open the terminal and run:
   ```bash
   docker --version
   ```

   Docker Desktop for macOS also comes with a graphical user interface (GUI) for easier management of containers and images.

---

### 3. **Installing Docker on Windows**

Docker Desktop is available for Windows 10 and Windows 11 (Pro, Enterprise, and Education editions). If you're using **Windows Home**, Docker Desktop requires Windows Subsystem for Linux 2 (WSL 2).

#### **For Windows 10/11 Pro, Enterprise, Education**

1. **Download Docker Desktop for Windows**  
   Visit the official Docker Desktop download page:  
   [Download Docker Desktop for Windows](https://www.docker.com/products/docker-desktop)

2. **Install Docker Desktop**  
   Run the installer and follow the on-screen instructions.

3. **Enable WSL 2 (if using Windows Home)**  
   For Windows Home users, Docker Desktop requires WSL 2. The installer will prompt you to install WSL and set WSL 2 as the default version if it's not already installed.

   - Open PowerShell as an administrator and run:
     ```bash
     wsl --set-default-version 2
     ```

4. **Launch Docker Desktop**  
   Once installation is complete, launch Docker from the Start menu. Docker will start running in the background, and you’ll see its icon in the system tray.

5. **Verify Docker Installation**  
   Open Command Prompt or PowerShell and run:
   ```bash
   docker --version
   ```

   You can also open Docker Desktop to verify everything is running smoothly.

#### **For Windows 10 Home Users (WSL 2 Required)**

If you are using Windows 10 Home, follow these additional steps to install Docker:

1. **Install WSL 2**  
   Docker Desktop requires Windows Subsystem for Linux (WSL 2) on Windows Home. To install WSL 2, you must first enable the WSL feature:
   - Open PowerShell as an administrator and run the following:
     ```bash
     wsl --install
     ```

2. **Set WSL 2 as Default**  
   After installation, run this command to make sure that WSL 2 is the default version:
   ```bash
   wsl --set-default-version 2
   ```

3. **Download and Install Docker Desktop**  
   Follow the same steps mentioned for Windows Pro and Enterprise to install Docker Desktop for Windows.

4. **Verify the Installation**  
   After installation, you can verify Docker by running:
   ```bash
   docker --version
   ```

---

### 4. **Installing Docker on Windows using Docker Toolbox (for older Windows versions)**

If you're using an older version of Windows (before Windows 10), you can install Docker Toolbox, which includes the Docker Engine, Docker CLI, Docker Compose, and VirtualBox.

1. **Download Docker Toolbox**  
   Visit Docker Toolbox’s official download page:  
   [Download Docker Toolbox](https://docs.docker.com/toolbox/toolbox_install_windows/)

2. **Install Docker Toolbox**  
   Run the installer and follow the prompts. It installs VirtualBox and other required tools.

3. **Verify the Installation**  
   Open the Docker Quickstart Terminal and run:
   ```bash
   docker --version
   ```

---

### 5. **Verifying Docker Installation**

Once Docker is installed, you can verify the installation by running the following command in your terminal or command prompt:

```bash
docker --version
```

To verify that Docker is running correctly, you can also run the `hello-world` container:

```bash
docker run hello-world
```

This command will pull a test image from Docker Hub (if it's not already available locally) and run it in a container. If everything is set up correctly, you’ll see a success message.

---

### Conclusion

Docker installation is straightforward across all major platforms (Linux, macOS, and Windows). Follow the appropriate steps for your system, and ensure you verify the installation by checking the Docker version and running a test container. Once Docker is installed, you can begin using containers for development, testing, and production deployments.
