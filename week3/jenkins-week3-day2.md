# Docker Image and Linux Commands

## Docker Image and Pushing to Docker Hub
After building the Docker image and pushing it to Docker Hub, we worked on Linux commands.

## Linux Commands

### Memory and CPU Usage
- `free -h` - Returns CPU usage in human-readable format (MB, GB), making it easier to interpret.
- `free -l` - Displays high and low memory status, which helps in understanding memory distribution.
- `free -w` - Adds buffer and cache separately, giving a clearer picture of available memory.
- `free -g` - Displays memory in gigabytes and rounds to the nearest number for convenience.
- `ps aux --sort -%mem | head` - Lists all processes sorted by memory usage and displays the top 10 processes, helping in identifying resource-intensive applications.
![image](https://github.com/user-attachments/assets/a40b324b-d236-4ac0-8ddf-cfc0ca93c901)
![image](https://github.com/user-attachments/assets/0e55db2e-b93b-4256-bbfa-1614aef3f579)

### Network Commands
- `ping chatgpt.com` - Checks if the website is reachable over the internet and measures response time.
- `ifconfig` - Displays and configures network interfaces, useful for diagnosing network issues.
- `ifconfig eth0` - Displays specific information about `eth0`, the primary network interface.
- `ip addr show` - Displays interface status, all interfaces, MAC addresses, broadcast addresses (supports IPv6 and IPv4), providing comprehensive networking details.
- `ip -4 addr show` - Displays only IPv4 addresses assigned to network interfaces.
- `ip -6 addr show` - Displays only IPv6 addresses assigned to network interfaces.
- `ip -br addr` - Displays a simplified view of all network interfaces and their assigned IPs for a quick overview.
![image](https://github.com/user-attachments/assets/cbaf1e98-9893-439a-a0dd-0cd751e6e277)

### System Performance and Package Management
- `sudo apt install stress` - Installs a CPU, memory, and disk stress-testing tool. It is useful for testing system stability under high loads.
- `sudo apt search firefox` - Searches for available Firefox-related packages in the system repository, useful for checking software availability.
![image](https://github.com/user-attachments/assets/03744103-b2c2-43a6-9ad9-16f7c385da3a)

## User and Group Management
```bash
sudo adduser username
sudo su -u username
sudo mkdir trying
sudo chmod 777 trying
sudo usermod -a -G c406cohort trying
sudo groupadd c406cohort
sudo mkdir -p /home/grouptry/username/a
sudo chmod 400 /home/grouptry/username/a
sudo chmod 400 /home/grouptry
sudo chgrp c406cohort /home/grouptry
sudo chgrp c406cohort /home/grouptry/username/a
sudo chmod 040 grouptry/
sudo chmod 2775 grouptry/
vi alpha.txt
sudo vi alpha.txt
```
- Creates another user and logs in.
- Creates a group and adds the user to the group.
- Modifies permissions and ownership for the group and user to control access rights.
- Creates a text file for testing file access permissions.

## SSH Key Generation and Git Clone
```bash
ssh-keygen -t rsa -b 4096 -C "kasuhema98@gmail.com"
cd .ssh/
ls -lrt
less id_rsa.pub
less id_rsa
cd
eval "$(ssh-agent -s)"
sudo apt install openssh-client
ssh-keygen -t ed25519 -C "kasuhema98@gmail.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
ssh -T git@github.com
git clone git@github.com:username/repository
```
- Generates SSH keys (public and private) for secure authentication.
- Public key is shared, whereas the private key remains confidential.
- Clones a Git repository using SSH to securely fetch project files.

## Jenkins Installation
```bash
# Update package lists
sudo apt update

# Install Java (required for Jenkins)
sudo apt install fontconfig openjdk-17-jre -y

# Install Jenkins
sudo apt install jenkins -y
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

# Add Jenkins user to Docker group (so Jenkins can run Docker commands)
sudo usermod -aG docker jenkins

# Restart Jenkins to apply group changes
sudo systemctl restart jenkins

# Access Jenkins in a browser
http://localhost:8080/login?from=%2F
```

![image](https://github.com/user-attachments/assets/3b5cb6df-ae72-4ecc-ba3d-aaac2fa39f93)

![image](https://github.com/user-attachments/assets/46c1026e-dfec-413c-ae74-9eedfe4fc42e)

- Installs Jenkins and Java dependencies, which are necessary for running Jenkins.
- Opens Jenkins in a browser via `localhost:8080`.
- Installs necessary plugins to extend functionality.
- Skips sign-in for now to quickly set up the environment.
![image](https://github.com/user-attachments/assets/e4364171-f34c-4467-ab9f-d8ee8a1290de)

## Conclusion
By following these steps, we successfully built and pushed a Docker image, explored essential Linux commands, managed users and groups, configured SSH for secure Git access, and installed Jenkins for CI/CD automation. These commands and setups are crucial for DevOps and software development workflows.
