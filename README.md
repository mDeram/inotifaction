# Inotifaction

A simple script/program launcher that call them when actions occurs on a watched directory.

It can be used to automate file management tasks.

## Dependency

1. A distribution using inotify.
2. Inotifywait, a program contained in the inotify-tools library.

## Installation

1. Install [inotify-tools](https://github.com/inotify-tools/inotify-tools) following the [installation instructions](https://github.com/inotify-tools/inotify-tools/blob/master/INSTALL)
2. Download the latest release of inotifaction
3. Run the install script:
```sh
./install [-c]	#The -c option stands for clean, meaning the downloaded folder will be removed.
```
4. Make sure the $HOME/.local/bin folder is in your path variable

## Usage Instructions

The config file is located at $HOME/.config/inotifaction/config, the syntax is the following:

- A line starting with '#' as its first character is a comment
- Empty lines are not interpreted
- Instructions line are composed of 3 strings separated by a semicolon:

> script_name;inotifywait arguments;/path/to/watched/directory

The script_name must match with a script contained in the $HOME/.inotifaction/scripts folder.

Inotifywait arguments can be found in the [man page](https://linux.die.net/man/1/inotifywait).

The /path/to/watched/directory must be an absolute path since relative path are not yet implemented.

Common inotifywait arguments you could need:
- "-m" the watch does not exit after a single event. The default behaviour is to exit after the first event.
- "-e \<event\>" listen for specific events only, the option can be used multiple times to specify multiple events to listen to. The default behaviour is to listen to all events. There is a list of the valid events in this [man page](https://linux.die.net/man/1/inotifywait)

### Scripts

Whenever an action occurs on a watched directory, the corresponding script is called (using the configuration file) with the following arguments:
```sh
/script_path/script_name watched_directory event(s) filename
```

- directory: the absolute path of the watched directory
- event(s): one or multiple events that happened on the file (in csv format)
- filename: the filename on which an event occured

### Inotifaction daemon

```sh
inotifactiond {start|stop|restart|status}
```

/!\ Do not start the daemon using ./inotifactiond, see the step 4 of the installation if you cannot run it without "./"

If you changed the configuration file, you must restart the daemon in order for changes to take place.

## Project Status

This project is subject to changes, feel free to open issues to request features/changes/bugfixes.
