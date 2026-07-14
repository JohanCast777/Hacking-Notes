Containerization is the process of packaging and running applications in isolated environments
# DOCKER

![[Pasted image 20260129201117.png|400]]

==WAYS TO USE DOCKER==

| Aspect                 | CLI            | GUI (Portainer) | TUI (LazyDocker) |
| ---------------------- | -------------- | --------------- | ---------------- |
| **Speed**              | ⚡ Fastest      | 🐢 Slower       | ⚡ Fast           |
| **Learning**           | Hard initially | Easy            | Easy             |
| **Scripts/Automation** | ✅ Yes          | ❌ No            | ✅ Yes            |
| **Pentesting labs**    | ✅ Perfect      | ❌ Overkill      | ✅ Perfect        |
| **Monitor containers** | Manual         | ✅ Dashboard     | ✅ Real-time      |
| **Remote SSH**         | ✅ Yes          | ✅ Web           | ✅ Yes            |
| **CTF/HackTheBox**     | ✅ Standard     | ❌ Unnecessary   | ✅ Good           |

 ==INSTALLATION==

Create a file with the name `install-docker.sh` that contains this
Kali linux
```bash
sudo apt update
sudo apt install ca-certificates curl gnupg -y
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo usermod -aG docker $USER
newgrp docker

```
Ubuntu
```
sudo apt update
sudo apt install ca-certificates curl gnupg -y
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo usermod -aG docker $USER
newgrp docker
docker run hello-world
```
Mint
```
sudo apt update
sudo apt install ca-certificates curl gnupg -y
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu jammy stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo usermod -aG docker $USER
newgrp docker
docker run hello-world
```

Use this commands to run the script
```
chmod +x install-docker.sh
```

```
sudo ./install-docker.sh -y
```

Install lazy docker
```
curl https://raw.githubusercontent.com/jesseduffield/lazydocker/master/scripts/install_update_linux.sh | bash
```

OPen lazydocker
```
~/.local/bin/lazydocker
```

Fix the patch 
```
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
```
```
export PATH="$HOME/.local/bin:$PATH"
```

Start docker
```
sudo systemctl enable --now docker
```

Create a group and assign the current user

```
sudo usermod -aG docker $USER
```
```
newgrp docker
```


==USAGE==

Create a project
Create the file wherever u want
```
mkdir myproject
cd myproject
```
```
nano docker-compose.yml
```
```
services:
  web:
    image: nginx
```
```
docker compose up -d
```
```
lazydocker
```

List docker images
```
docker images
```

Install image (Image.iso)
```
docker pull ubuntu:22.04
```

```
 docker pull kalilinux/kali-rolling
```

Create your own image (100% reproducible environment.)
```
docker build -t my-kali-tools .
```

Remove images 
```
docker rmi IMAGE_ID_OR_NAME
```
Force
```
docker rmi -f IMAGE_ID_OR_NAME
```

Additional set up
```
-t name:tag
```
Custome docker name file
```
-file fille
```

List all the Containers (-a=Stopped)
```
docker ps -a
```

Create a container
```
docker run -it --name test-ubuntu ubuntu:22.04 bash
```

Create a container in the background
```
docker run -d --name web nginx
```

Start a container
```
docker start test-ubuntu
```

Stop a container
```
docker stop test-ubuntu
```

Remove a container
```
docker rm -f web
```

| Flag                | Example           | Meaning                                  |
| ------------------- | ----------------- | ---------------------------------------- |
| `-it`               | `-it bash`        | Interactive terminal (for shells, tools) |
| `-d`                | `-d nginx`        | Detached (background)                    |
| `--name`            | `--name mylab`    | Human‑readable name                      |
| `-p host:container` | `-p 8080:80`      | Port mapping (host→container)            |
| `-v host:container` | `-v ~/data:/data` | Bind mount (share files)                 |
| `--rm`              | `--rm`            | Auto‑remove when container exits         |

Rootless Docker

| Command                                                                      | Explanation                                                                              |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `sudo apt install -y uidmap dbus-user-session`                               | Installs packages required for rootless Docker (user namespaces, dbus session).          |
| `sudo apt install -y docker-ce docker-ce-rootless-extras`                    | Installs Docker Engine and the extra tools for rootless mode (if not already installed). |
| `dockerd-rootless-setuptool.sh install`                                      | Sets up a rootless Docker daemon in your home directory.                                 |
| `systemctl --user start docker`                                              | Starts the **rootless** Docker daemon as a user service.                                 |
| `systemctl --user enable docker`                                             | Starts rootless Docker automatically each time you log in.                               |
| `loginctl enable-linger $USER`                                               | Allows your user services (like rootless Docker) to stay running even when you log out.  |
| `echo 'export DOCKER_HOST="unix:///run/user/1000/docker.sock"' >> ~/.bashrc` | Points the `docker` CLI to the rootless Docker daemon socket (UID 1000 example).         |
| `docker info`                                                                | Shows detailed info; will say `rootless: true` when you’re talking to rootless Docker.   |
Use the container terminal
```
docker attach "name container"
```

Start lazydocker
```
lazydocker
```





==OTHER TECHNOLOGIES FOR CONTAINERIZATION==

LXC
Podman
Rootless Docker (Most secured, and anonym)
Rootless Podman (Most secured, and anonym)

