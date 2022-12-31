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

