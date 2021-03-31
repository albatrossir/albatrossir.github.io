## Albatross

Albatross is a remote access tool specifically designed for enabling Host Forensics investigations and threat hunting on remote endpoints. Albatross was designed to be as simple to use as possible, while providing an extendable platform to build tooling on. 

It consists of two components. A restful API Server built to a single executable for portability, and an Endpoint Agent, currently supporting Windows 7 and 10 with future support planned for OSX and Debian Based Systems.

### The Server

The Server is a standalone executable, designed to be as portable as possible with low system requirements. It uses a sqlite backend which we have found to be sufficient for a large number of endpoints.

The Server exposes two API's, the first for the endpoint agent, the second for analysis tools.

The API Specs can be found [Here](swagger/index.html)


### The Endpoint

The endpoint agent is responsible for providing data, and executing tasks to the API


## Installation

- Download latest release.
- `albatross.exe --init`
    - Creates the relevant databases and directories, creates an administrative user and generates SSL keys.
- `albatross.exe --fingerprint`
    - Displays the SSL Fingerprint you'll need to feed to the endpoint installer
- `albatross.exe --runserver`
    - Runs the server..
