# Born2BeRoot Project Overview

## Project Concept
System administration and virtualization project focusing on Linux server configuration and security.

## Part 1: Operating System Setup
### Core Objectives
- Install minimal Debian/Rocky Linux
- Configure secure system environment
- Implement advanced partition strategies
- Set up LVM (Logical Volume Management)
- Configure strong user/group permissions

### Technical Requirements
- Specific disk partitioning scheme
- No graphical interface
- UFW firewall configuration
- SSH service management
- System hardening techniques

## Part 2: Monitoring Script (monitoring.sh)

### Monitoring Script Functionality
Comprehensive system information collector:

#### System Metrics
- Architecture details
- CPU information
  - Physical/virtual CPU count
- Memory utilization
- Disk usage
- CPU load
- Boot timestamp
- LVM status
- Network connections
- Active user sessions
- Network interface details
- Sudo command tracking

#### Technical Implementation
- Uses Linux command-line utilities
- Real-time metric collection
- Broadcasts system report to users

### Key Configuration Points
- Secure information display
- Automated periodic execution
- Minimal system overhead
- Standardized reporting format

-------------------------------------------------------------
# Monitoring Script Detailed Explanation

## Purpose
Comprehensive system information gathering script for Linux environments.

## Technical Components

### System Architecture
- Retrieves system architecture details
- Command: `uname -a`

### CPU Information
- Physical CPU count
  - Uses `/proc/cpuinfo`
  - Command: `grep "physical id" | wc -l`
- Virtual CPU count
  - Command: `grep "processor" | wc -l`

### Memory Utilization
- Total memory calculation
- Used memory percentage
- Uses `free -m` command
- Calculates percentage: `(used/total) * 100`

### Disk Usage
- Total disk space
- Used/free space percentage
- Command: `df --total -h`

### Performance Metrics
- CPU load tracking
- Last system boot time
- Command: `uptime`
- Command: `who -b`

### Network Details
- IP address
- Network interface
- MAC address
- Commands: `hostname -I`, `ip route`, `ip address`

### Security Monitoring
- LVM status check
- TCP connections
- Active user sessions
- Sudo command tracking

### Reporting Mechanism
- Uses `wall` command
- Broadcasts information to all logged-in users
- Formatted, human-readable output

## Key Technical Approaches
- Bash scripting
- Command-line utility parsing
- Dynamic information retrieval
- Real-time system analysis
