# Docker High Availability Failover Lab
## Project Overview
### Disclaimer  
    The company name, logo, branding, and website content used in this project are entirely fictional and were created solely for educational and demonstration purposes.  
    Any resemblance to existing organizations, products, or trademarks is purely coincidental.
  
This project demonstrates a simple High Availability (HA) and Disaster Recovery (DR) implementation using Docker Compose and Nginx.
A reverse proxy (Nginx) acts as the front-end load balancer and routes incoming requests to the primary web server. If the primary server becomes unavailable, Nginx automatically redirects traffic to a backup recovery server using its built-in passive health check and backup server functionality
The goal of this project is to simulate service continuity during server failures while providing hands-on experience with container networking, reverse proxies, and failover concepts.

<img width="800" height="450" alt="Lab Diagram" src="https://github.com/user-attachments/assets/e6b5c890-5ded-4818-8df3-d09780cb1450" />

## Features
- Docker Compose deployment
- Nginx reverse proxy
- Automatic failover
- Passive health checking
- Backup web server
- Isolated Docker bridge network
- Simple Disaster Recovery simulation
- Easy deployment using containers

## Technology Used
| Technology | Purpose |
| -- | -- |
| Docker Compose | Container orchestration |
| Docker | Containerization |
| Nginx | Reverse Proxy | 
| Linux | Container Environment | 
| Bridge Networking | Internal Communication | 

## Working
- Client sends an HTTP request to localhost:8080.
- Nginx receives the request.
- Nginx forwards traffic to the Primary Server.
- If the primary server becomes unavailable, Nginx marks it as failed after one unsuccessful attempt (max_fails=1).
- During the configured fail_timeout period (5 seconds), Nginx automatically forwards requests to the Recovery Server.
- Once the primary server becomes healthy again, it becomes eligible to receive requests after the fail timeout.

## Nginx Failure Configuration

    upstream backend_servers 
    {
    server primary-server:80 max_fails=1 fail_timeout=5s;
    server recovery-server:80 backup;
    }

## Explanation
- max_fails=1
  - Marks the primary server as unavailable after one failed request.
- fail_timeout=5s
  - Keeps the failed server out of rotation for five seconds before retrying it.
- backup
  - The recovery server only receives traffic when the primary server is unavailable.
 
# Running the project
## Cloning the repository
    git clone https://github.com/Kexelex/Nginx-Failover-Disaster-Recovery-Simulation.git

## Navigating to repository 
    cd Docker-High-Availability-Failover-Lab

## Starting a container
    docker compose up -d

## Verify the running container
    docker ps

## Opening WebUI 
    http://localhost:8080

# Simulating Failover
## Stop primary server
    docker stop primary_hr_db

Refresh the browser.
The Recovery Server page should now be displayed automatically.

## Simulating Failback
    docker start primary_hr_db
Starting the primary server back on.  
Wait approximately five seconds for the fail timeout to expire, then refresh the browser.  
Traffic will again be served by the Primary Server.  

## Learning Outcomes
This project helped reinforce practical knowledge of:
- High Availability principles
- Disaster Recovery concepts
- Docker networking
- Reverse proxies
- Nginx upstream configuration
- Containerized infrastructure
- Service resilience
- Fault tolerance

## Skills Demonstrated
- Docker
- Docker Compose
- Nginx
- Reverse Proxy Configuration
- High Availability
- Disaster Recovery
- Linux Administration
- Infrastructure Resilience
- Network Fundamentals
