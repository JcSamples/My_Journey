
# Process Monitoring and Management Commands

## Viewing Running Processes
- **Command:** 
```bash
ps
```
- **Description:** Displays the currently running processes in the shell. This command gives a snapshot of active processes and their respective details, such as PID (Process ID), TTY (terminal type), time, and command name.

## Listing Signal Numbers
- **Command:** 
```bash
kill -l
```
- **Description:** Lists all the signal names and their corresponding numbers. Useful for knowing which signal to send with the `kill` command.

## Adjusting Process Priority
- **Command:** 
```bash
nice
renice
```
- **Description:** 
  - `nice` is used to start a process with a specified priority.
  - `renice` changes the priority of an already running process. Lower values mean higher priority.

## Managing Multiple Terminals
- **Command:** 
```bash
screen
```
- **Description:** Allows you to manage multiple shell sessions within a single terminal window. You can create new sessions, switch between them, and even detach and reattach to sessions as needed.

# Monitoring System Performance

## Viewing System Processes and Resource Usage
- **Command:** 
```bash
top
```
- **Description:** Displays a dynamic view of the system’s processes and resource usage, such as CPU and memory usage. Processes are ordered by CPU usage by default.

- **Command:** 
```bash
htop
```
- **Description:** An improved version of `top`, `htop` provides a more user-friendly interface and additional functionality, such as mouse interaction and customizable display options.

## Checking System Uptime
- **Command:** 
```bash
uptime
```
- **Description:** Displays how long the system has been running, along with the current time, number of logged-in users, and the load averages for the past 1, 5, and 15 minutes.

## Displaying Kernel Module Information
- **Command:** 
```bash
modinfo
```
- **Description:** Shows information about a Linux kernel module. It displays details such as the module name, description, license, author, and dependencies.

## Searching for Processes by Name
- **Command:** 
```bash
pgrep -i
```
- **Description:** Searches for processes by name, with case insensitivity. This is useful when you know part of a process name but aren't sure about its case.

# Memory Management

## Viewing Memory Usage
- **Command:** 
```bash
free -c [count]
```
- **Description:** Displays the system’s memory usage, with the option to repeat the command `[count]` number of times. Useful for monitoring memory in real-time.

- **Command:** 
```bash
cat /proc/meminfo
```
- **Description:** Shows detailed information about the system’s memory usage directly from the `/proc/meminfo` file.

- **Command:** 
```bash
cat /proc/cpuinfo
```
- **Description:** Displays information about the CPU(s) on your system, including vendor ID, model, frequency, and more.

## Managing Disk Partitions
- **Command:** 
```bash
fdisk [-l];[-x]
```
- **Description:** 
  - `-l` lists the partition tables of all disks.
  - `-x` provides extra details about the partitions, useful for advanced disk management tasks.

# Hardware Information and System Search

## Listing USB Devices
- **Command:** 
```bash
lsusb
```
- **Description:** Displays information about USB buses in the system and the devices connected to them. It’s helpful for identifying connected peripherals.

## Displaying CPU Information
- **Command:** 
```bash
lscpu
```
- **Description:** Shows detailed information about the CPU architecture, including the number of cores, threads, architecture type, and more.

## Listing PCI Devices
- **Command:** 
```bash
lspci
```
- **Description:** Lists all PCI devices on the system. This command is useful for troubleshooting hardware-related issues or checking hardware configurations.
