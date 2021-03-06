<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-Z42R8RP1E5"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-Z42R8RP1E5');
</script>

## Albatross

Albatross is a remote access tool specifically designed for enabling Host Forensics investigations and threat hunting on remote endpoints. Albatross was designed to be as simple to use as possible, while providing an extendable platform to build tooling on. 

It consists of two components. A restful API Server built to a single executable for portability, and an Endpoint Agent, currently supporting Windows 7 and 10 with future support planned for OSX and Debian Based Systems.

Longer term, the code may be made open source (once it's at a state of tidiness befitting an open source project). For now, the documentation is open for development on top of the server API.

Any issues can be reported [here](https://github.com/albatrossir/albatrossir.github.io/issues).

A short and super professional video demo can be found [here](https://vimeo.com/533625161)

### The Server

The Server is a standalone executable, designed to be as portable as possible with low system requirements. It uses a sqlite backend which we have found to be sufficient for a large number of endpoints.

The Server exposes two API's, the first for the endpoint agent, the second for analysis tools.

The API Specs can be found [here](swagger/index.html).


### The Endpoint

The endpoint agent is responsible for providing data, and executing tasks to the API.

By default it will also collect Windows event logs, and take a full Snapshot once per 24 hours, including a file listing, with MD5 and SHA256 file hashes.

The endpoint will install and set itself to run as a system level service.


## Installation

- Download latest release.
- `albatross_server_linux_64 --init`
    - Creates the relevant databases and directories, creates an administrative user and generates SSL keys.
- `albatross_server_linux_64 --fingerprint`
    - Displays the SSL Fingerprint you'll need to feed to the endpoint installer
- `albatross_server_linux_64 --runserver`
    - Runs the server..

## Agent Install

As administrator:

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


## Changelog

### 0.03 xx/xx/xxxx
- 23/08/2021: Bugfix - Various
- 23/08/2021: Enhancement [#23](https://github.com/albatrossir/albatrossir.github.io/issues/23): Query snapshot data
- 23/08/2021: Enhancement [#5](https://github.com/albatrossir/albatrossir.github.io/issues/5): Implement Log Search API Endpoint

### 0.02 19/07/2021
- 19/07/2021: Bugfix [#22](https://github.com/albatrossir/albatrossir.github.io/issues/22): Fix Bug where Provider.Name contains a space
- 19/07/2021: Enhancement [#8](https://github.com/albatrossir/albatrossir.github.io/issues/8): Allow Requesting data by snapshot.
- 07/07/2021: Bugfix [#1](https://github.com/albatrossir/albatrossir.github.io/issues/1): Crash on file fetch
- 07/07/2021: Enhancement [#4](https://github.com/albatrossir/albatrossir.github.io/issues/4): Rotate Snapshots
- 07/07/2021: Enhancement [#10](https://github.com/albatrossir/albatrossir.github.io/issues/10): Add User Function
- 03/06/2021: Bugfix - Expired api keys causing error.
- 25/05/2021: Engancement [#20](https://github.com/albatrossir/albatrossir.github.io/issues/20): Store Logs per date.
- 21/05/2021: Enhancement [#19](https://github.com/albatrossir/albatrossir.github.io/issues/19): Text Wrapping in Albatross CLI Tool
- 21/05/2021: Enhancement [#17](https://github.com/albatrossir/albatrossir.github.io/issues/17): Log Sync Frequency adjusted
- 20/05/2021: Bugfix [#18](https://github.com/albatrossir/albatrossir.github.io/issues/18): Binary Files Causing Crash
- 19/05/2021: Bugfix [#12](https://github.com/albatrossir/albatrossir.github.io/issues/12): Agent Logging Verbosity
- 19/05/2021: Bugfix [#15](https://github.com/albatrossir/albatrossir.github.io/issues/15): Windows Agent Service Install Type
- 19/05/2021: Enhancement [#6](https://github.com/albatrossir/albatrossir.github.io/issues/6): Event Log Normalisation
- 14/05/2021: Bugfix [#14](https://github.com/albatrossir/albatrossir.github.io/issues/14) : Inconsistent snapshots caused by flawed implementation of time check.
- 11/05/2021: Enhancement [#3](https://github.com/albatrossir/albatrossir.github.io/issues/3) : CLI Tool File Timestamps.
- 11/05/2021: Bugfix [#13](https://github.com/albatrossir/albatrossir.github.io/issues/13): Error when listing snapshots that do not exist.
- 11/05/2021: Bugfix [#9](https://github.com/albatrossir/albatrossir.github.io/issues/9): Error when running ls with no snapshot
- 11/05/2021: Enhancement [#7](https://github.com/albatrossir/albatrossir.github.io/issues/7): Added piping to command line with support for `more` and `grep`

### 0.01 06/04/2021

Initial Release
