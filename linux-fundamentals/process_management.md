## Processes
- Everything in linux is a process
- You can view the running processes with their resource utilizations in a system using the `top` command
- A process is an instance of a program executed from memory
- A process tree is formed when proceses are created. there are child and parent processes
- `systemd` is the grandfather of all processes. It is the only process started directly by the kernal
- To see processes started by you use `ps`
- To see processes by all the users use, `ps -e`
- To see heirarchies use `ps -H`
- More info: `ps -f` or `ps -F` or `ps -lf`
- Use `--sort` and `--format` options for sorting and formatting the output
- Eg `ps -e --format uid,pid,tty,%cpu,cmd --sort %cpu`
- Killing a process: SIGTERM is a friendly way of killing a process. SIGKILL forcebaly kilss a process
- To view `top` with a better UI, use `htop`

### Top commands
- Press `f` to change the fields
- Press `M` or `P` or `C` ... to sort the rows by Memory, PID, or CPU utilization respectively
- Press `u` to filter by a user
- Press `k` to kill a process
- Press `r` to renice a process

- Processes are scheduled in Linux by the scheduler. It uses the Process priority (0 - 99), higher the priority value lower the priority. 
- You can change the priority of a process by changing its niceness value (-20 - 19). The net priority is the sum of the niceness and the priority value. To increase the priority, use `renice -n <value> <pid>` and provide a negative value. Thi will bring down the overall priority. To provide a negative value, you need to use the command as a privilleged user (use `sudo`)

### Kill Process
- To get the pid of a process, use `pgrep <process_name>` command
- Show the process tree: `pstree`
- Kill all processes with the same name: `killall <pid>`
- Kill all processes by a user: `killall -u <user_name>`

### Jobs
- Use `watch` command to periodically run a command and see the updates
- See the active jobs: `jobs`
- Start a process in the background: `<command to start> &`
- Put a running process in the background: Press Ctrl + Z to suspend it and then press `bg`
- Kill a job and all its subprocesses: `kill $<job_id>`
- Bring a running process to the foreground: `fg $<job_id>`
- Bring a running process to the background: `bg $<job_id>`

### System Services
- Called a `Daemon`, these are services that run in the background waiting for a request. These proceses are started in the background by the system, when it boots up
- The kernel starts a super service that manages all the other system services: 
      - Traditionally, this super service was `init`. This became slow as it started synchronously and can only used for boot up tasks. 
      - Modern systems use `systemd` that is a suite of services that handle, manage and asynchronously start system services. It includes the init system
      - It aims to unify bootup in different distributions
      - It not only manages services, but also, networks, storage etc. and replaces a lot of other daemons

### Systemd
- Systemd has different units that it manages, These are managed using their unit files
- You can use `systemctl status <unit>` to view the status of a unit
- Use `systemctl cat <unit>` lists the content of the unit file
- Using `systemctl list-units` will list the running units
- Use `systemctl list-unit-files [-t service]` to get a list of unit files, running or not
- You can `start` or `stop` or `restart` a service with systemctl, but these changes won't persist
- To persist changes you can, `mask`: Cannot be manually started or automatically or `disable`: Cannot be automatically started but manually yes

### Init System
- WSL doesn't have systemd by default and to start and stop services, you can use:
- `service start <name>` and `service stop <name>`
- Use `service status <name>` to check the status of a service

## Job Scheduling
### One-time jobs with `at`
- `at teatime`
- `atq`: List jobs
- Batch jobs: Run only when the system's load avg drops below 0.8
- Bath jobs using `batch`

### Cron Jobs: reccuring
- `crontab` is the command used to submit jobs to the cron service
- user and system-wide
- ![image](https://user-images.githubusercontent.com/54491362/210163774-01af467a-e72b-4c63-9ccc-97d26170f0fb.png)
- `man 5 crontab` for the crontab syntax
- https://crontab-generator.org/
![image](https://user-images.githubusercontent.com/54491362/210163962-5ce4a414-5fe1-4ba7-bc0c-be3f80b9c121.png)
- System wide cron files are stored in `/etc/cron.d/<file>`
- You can allow or deny access to cron and at using `/etc/at.allow` or `/etc/cron.allow` or `/etc/at.deny` or `/etc/cron.deny`
- Allow overwrites deny. By default there is an empty deny file and no allow file. An empty allow file won't allow anyone and the lack of a deny file will deny everyone.
- You can also use `access.conf` to control access of users to a command. Refer to `man access.conf`

### Systemd timers
- Realtime timers: Calendar events (date and time value)
- Monotonic timer: After a timespan relative to a starting point. Eg. 5 min after boot
- Jobs can be configured to run wrt an event or in their own environment when using systemd timers
- List timers: `systemctl list-timers`


## Date Time in Linux
- Linux has OS time and Hardware time. These have to be synchronized with each other for normal functioning. 
- There shouldn't be a difference of more than 1000s.
- You can see and format the datetime with `date [+%d-%m-%Y]` command
- You can use `sudo hwclock` to view the hwtime and use `sudo hwclock --systohc`
- Use `timedatectl` to manage time
