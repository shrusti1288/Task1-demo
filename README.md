# Task1-demo
Automate Code Deployment Using CI/CD Pipeline (GitHub Actions)

Step-by-Step Guide to Install Netdata Using Docker

1. Install Docker (if not already installed)

Follow official instructions:
https://docs.docker.com/get-docker/

2. Pull and Run Netdata Container

docker run -d \
  --name=netdata \
  -p 19999:19999 \
  -v netdataconfig:/etc/netdata \
  -v netdatalib:/var/lib/netdata \
  -v netdatacache:/var/cache/netdata \
  -v /etc/passwd:/host/etc/passwd:ro \
  -v /etc/group:/host/etc/group:ro \
  -v /proc:/host/proc:ro \
  -v /sys:/host/sys:ro \
  -v /etc/os-release:/host/etc/os-release:ro \
  --cap-add SYS_PTRACE \
  --security-opt apparmor=unconfined \
  netdata/netdata

> This command runs Netdata on port 19999. It mounts necessary volumes for system metrics access.



3. Access the Netdata Dashboard

Open your browser and go to:
http://localhost:19999

You should see a live, interactive dashboard showing:

CPU, RAM, Disk usage

Network traffic

Application-specific metrics

Docker container stats (if Docker plugin is active)


4. Take a Screenshot

Once the dashboard is up and

