# Enterprise HAProxy Load Balancer with Real-Time Monitoring

## Project Overview

This project demonstrates an enterprise-level implementation of a High Availability Load Balancing architecture using HAProxy. The system distributes incoming user traffic across multiple backend web servers using the Round Robin algorithm while providing real-time monitoring through HAProxy Stats.

The project is deployed on VMware virtual machines and simulates a real-world enterprise environment.

---

## Objectives

* Implement Load Balancing using HAProxy.
* Distribute traffic using Round Robin algorithm.
* Host two independent web applications.
* Monitor server health in real time.
* Simulate enterprise architecture.
* Implement backend health checks and failover.

---

## Architecture

```text
                 User Browser
                       |
                       |
             Public IP (HAProxy)
                       |
               VM1 Load Balancer
               HAProxy + Stats
                       |
          -------------------------
          |                       |
          |                       |
VM2 Cloud Service Node    VM3 Cyber Service Node
     Apache Web Server      Apache Web Server
```

---

## Virtual Machine Architecture

### VM1 : HAProxy Load Balancer

Responsibilities:

* Receives all user requests
* Uses Round Robin algorithm
* Performs health checks
* Hosts HAProxy Stats dashboard
* Exposes one public IP

Software:

* Ubuntu 22.04
* HAProxy

---

### VM2 : Cloud Service Node

Responsibilities:

* Hosts custom website
* Acts as Backend Pool Server 1

Software:

* Ubuntu 22.04
* Apache2
* HTML
* CSS

---

### VM3 : Cyber Service Node

Responsibilities:

* Hosts custom website
* Acts as Backend Pool Server 2

Software:

* Ubuntu 22.04
* Apache2
* HTML
* CSS

---

## Technologies Used

* VMware
* Ubuntu 22.04
* HAProxy
* Apache2
* HTML
* CSS
* Git
* GitHub

---

## Load Balancing Algorithm

### Round Robin

Incoming requests are distributed sequentially.

Example:

Request 1 → VM2

Request 2 → VM3

Request 3 → VM2

Request 4 → VM3

This ensures equal traffic distribution.

---

## HAProxy Monitoring Dashboard

Dashboard URL:

```text
http://LOAD-BALANCER-IP:8404/stats
```

Monitored parameters:

* Backend Server Status
* Active Sessions
* Request Count
* Health Checks
* Response Time
* Server Availability

---

## Health Check Configuration

Health checks continuously verify backend server availability.

Configuration:

```text
default-server inter 3s fall 3 rise 2
```

Meaning:

* inter 3s = Check every 3 seconds
* fall 3 = Mark DOWN after 3 failures
* rise 2 = Mark UP after 2 successful checks

---

## Failover Testing

If VM2 goes offline:

```text
systemctl stop apache2
```

HAProxy automatically redirects all traffic to VM3.

When VM2 comes back online:

```text
systemctl start apache2
```

Traffic distribution resumes automatically.

---

## Useful Commands

### Install Apache

```bash
apt update
apt install apache2 -y
```

### Install HAProxy

```bash
apt update
apt install haproxy -y
```

### Check HAProxy Configuration

```bash
haproxy -c -f /etc/haproxy/haproxy.cfg
```

### Restart HAProxy

```bash
systemctl restart haproxy
```

### Check HAProxy Status

```bash
systemctl status haproxy
```

### Start Apache

```bash
systemctl start apache2
```

### Stop Apache

```bash
systemctl stop apache2
```

---

## Project Features

* Enterprise Architecture
* HAProxy Load Balancing
* Round Robin Algorithm
* Real-Time Monitoring
* Backend Health Checks
* Automatic Failover
* Attractive Web Interfaces
* VMware Deployment
* GitHub Integration

---

## Future Enhancements

* SSL/HTTPS
* Reverse Proxy
* Logging Server
* Prometheus Monitoring
* Grafana Dashboards
* DNS Integration

---

## Contributors

* Chand Parveen
* Friend Name
