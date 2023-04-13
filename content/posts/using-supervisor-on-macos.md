---
title: "Using Supervisor on macOS"
date: 2023-04-13T10:45:32-07:00
draft: false
tags:
- macos
---

When I'm working on a project, I often need to run a number of processes, e.g. a frontend app, several backend services, maybe a redis server etc. Instead of running them in Docker containers, or in separate terminal windows, I like to use [Supervisor](http://supervisord.org/). Supervisor is a process control system on UNIX-like OSes, and is easy to use on macOS.

### Installation
The simplest option is to use [pip](https://pypi.org/project/pip/):

```shell
pip3 install supervisor
```

Other options for installation are available [here](http://supervisord.org/installing.html).

### Creating a Configuration File
You can create a sample configuration file using `echo_supervisord_conf`.

```shell
echo_supervisord_conf > /path/to/supervisord.conf
```

Customize the file as appropriate. I leave the default sections as-is, just add my programs:

```ini
[program:redis-server]
command=/path/to/redis-server
autostart=false
autorestart=true
stdout_logfile=/path/to/logs/redis-server.log
stderr_logfile=/path/to/logs/redis-server.err.log
```

Finally, I like to create a symbolic link in `/etc/` so supervisor can automatically find the file. This is not required, it just saves me from having to type the full path every time.

```shell
sudo ln -s /path/to/supervisord.conf /etc/supervisord.conf
```

### Running supervisord
Now we are ready to start the server:

```shell
supervisord
```

If you didn't create a symlink in one of the default paths where supervisord searches for the config file, you can also specify the config path on the command line:

```shell
supervisord -c /path/to/supervisord.conf
```

### Running supervisorctl
You interact with supervisord using `supervisorctl`:

```shell
$ supervisorctl status
redis-server                     STOPPED   Not started
```

Or if the config file is not in a standard location:

```shell
$ supervisorctl -c /path/to/supervisord.conf status
redis-server                     STOPPED   Not started
```

#### Managing the processes
You can a variety of commands with supervisorctl to manage the processes, including `start`, `stop`, `restart`, `status` and `reload`. To get a full list of commands, type:

```shell
supervisorctl help
```

### Creating an alias
Finally, I create a helper function to save myself a few keystrokes every time I need to start, stop or restart a process. Something like this:

```shell
sup() {
  if (( $# == 0 )) then
    cd /path/to/logs
  fi
  case "$1" in
    "logs") cd /path/to/logs
    ;;
    "status") supervisorctl status
    ;;
    "start")
      case "$2" in
        "all")
          supervisorctl start redis-server
        ;;
        "redis")
          supervisorctl start redis-server
        ;;
        *) supervisorctl start $2
        ;;
      esac
      ;;
    "stop") ;&
    "restart")
      case "$2" in
        "redis")
          supervisorctl $1 redis-server
        ;;
        *) supervisorctl $1 $2
        ;;
      esac
  esac
}
```

Now I can type:

```shell
sup status
sup start redis
sup stop redis
sup restart redis
```

That's it!
