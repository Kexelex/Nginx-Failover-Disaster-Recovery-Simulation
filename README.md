# Docker High Availability Failover Lab
## Project Overview
This project demonstrates a simple High Availability (HA) and Disaster Recovery (DR) implementation using Docker Compose and Nginx.
A reverse proxy (Nginx) acts as the front-end load balancer and routes incoming requests to the primary web server. If the primary server becomes unavailable, Nginx automatically redirects traffic to a backup recovery server using its built-in passive health check and backup server functionality
The goal of this project is to simulate service continuity during server failures while providing hands-on experience with container networking, reverse proxies, and failover concepts.

