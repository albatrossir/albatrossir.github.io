## Albatross

Albatross is a remote access tool specifically designed for enabling Host Forensics investigations and threat hunting on remote endpoints. Albatross was designed to be as simple to use as possible, while providing an extendable platform to build tooling on. 

It consists of two components. A restful API Server built to a single executable for portability, and an Endpoint Agent, currently supporting Windows 7 and 10 with future support planned for OSX and Debian Based Systems.

### The Server

The Server is a standalone executable, designed to be as portable as possible with low system requirements. It uses a sqlite backend which we have found to be sufficient for a large number of endpoints.

The Server exposes two API's, the first for the endpoint agent, the second for analysis tools.

The API Specs can be found [Here](swagger/index.html) OLD VERSION BEWARE!


### The Endpoint

The endpoint agent is responsible for providing data, and executing tasks to the API


## Installation

- Download latest release.
- `albatross_server_linux_64 --init`
    - Creates the relevant databases and directories, creates an administrative user and generates SSL keys.
- `albatross_server_linux_64 --fingerprint`
    - Displays the SSL Fingerprint you'll need to feed to the endpoint installer
- `albatross_server_linux_64 --runserver`
    - Runs the server..

## Agent Install

- `albatross_installer_windows <ip address> <port> <fingerprint>`
    - Installs Albatross to %PROGRAMFILES%\Albatross

## CLI Tool

Supported Commands

#### Top Level Commands
- `connect` - Connect to the albatross server
- `hosts` - List hosts
- `use <host_id>` - Select a host to work on
- `exit` - Exit
#### Host Level Commands
- `info` - Show information about the host
- `persistence` - Get a list of persistence mechanisms (Services, Autoruns etc)
- `processes` - Get a list of running processes
- `netstat` - Get a list of network connections
- `isolate` - Quarantine the endpoint from any communications other than the albatross server
- `release` - Release the endpoint from quarantine
- `ls` - list directory
- `tasks` - Show a log of tasks and status'
- `snapshots` - Show snapshots that have been taken of the host
- `cd <directory>` - change directory
- `cwd` - print current directory
- `get <filename/filepath>` - Downloads a file from the current directory, or from a path if specified
- `back` - stop working on a host
