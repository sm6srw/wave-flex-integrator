# Wave-Flex-Integrator

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Node.js Version](https://img.shields.io/badge/node.js-12%2B-green.svg)](https://nodejs.org/)

A powerful tool that connects your FlexRadio to the Wavelog logging software, integrating DX Cluster data and seamlessly syncing frequency and mode without the need for traditional CAT software. It simplifies your setup, allowing you to focus more on operating and logging your contacts.

> **Note:** This software is currently in beta testing, and the information below may be updated frequently as the project evolves.

> **Note:** The TNXQSO team is not affiliated with **Wavelog** or **FlexRadio**. This project is independently developed to integrate these tools for the ham radio community.

> **Note:** This software is currently not listening for logging ADIF brodcasts from programs like WSJT-X but it's a feature that we are considering to add. If you run digital modes, you might want to wait until we've added that functionality.


## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Requirements](#requirements)
- [What is Wavelog](#what-is-wavelog)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgments](#acknowledgments)

## Introduction

Tired of running multiple programs just to log contacts and integrate with FlexRadio? If you're using [Wavelog's web based Logging Software](https://www.wavelog.org) this tool eliminates the need for CAT software by directly syncing your radio and logging software. **Wave-Flex Integrator** connects to a DX Cluster, processes incoming spots, and enhances them with additional information via the Wavelog API before sending them to your FlexRadio.

When a spot appears on your SmartSDR panadapter, you can click it, and a prefilled Wavelog logging window will open, ready to log the QSO. This application works exclusively with **Wavelog** and **FlexRadio**, and we are not affiliated with either of them. Currently, it supports no other logging software.

## Features

- **DX Cluster Integration**: Automatically connect to a DX Cluster to receive real-time spot data.
- **Spot Augmentation**:
  - Enriches spot data using the Wavelog API, showing whether a callsign’s DXCC is needed for the band or mode, and whether they are a LoTW (Logbook of The World) member.
  - Sends color-coded spots to FlexRadio’s SmartSDR panadapter. Colors can be customized based on DXCC, worked-before status, and LoTW membership.
- **One-Click Logging**: Clicking a spot in SmartSDR opens a Wavelog logging window with the callsign and relevant data prefilled.
- **Error Handling**: Automatically reconnects to the DX Cluster and FlexRadio if the connection drops.
- **Seamless FlexRadio and Wavelog Sync**: Automatically syncs frequency and mode between FlexRadio and Wavelog without the need for CAT software.
- **Cross-Platform Support**: Aims to support Windows, macOS, and Linux.

## Requirements

- **Node.js**: Version 12 or higher for running the application.
- **NPM**: Node Package Manager for installing dependencies.
- **FlexRadio**: Compatible FlexRadio device connected to your LAN or reachable on the Internet over TCP-IP. You sholud enable spots in Settings --> Spots. Do not override colors or background.
- **SmartSDR**: Installed and running on your local machine. Version 3.7.4 or higher is tested. Find your version in Settings --> Radio setup --> Radio tab -->Radio Hardware version, (Yes, Radio Hardware version) which is the version of SmartSDR that is running and the associated radio firmware.
- **WaveLog**: Installed and running with the `dev` branch checked out [as described above](#how-to-switch-to-the-wavelog-dev-branch)
- **DX Cluster Access**: Your callsign will be used to access a DX Cluster server of your choice.

> **Note:** While we provide the source code for those who want to run it via Node.js, we will soon offer binaries for easier installation. At the time of writing, Wavelog’s main repository has not yet merged the new API features required. You can, however, use Wavelog’s development branch, where these features are already included. Stay tuned for updates on this.

## What is Wavelog?

**Wavelog** is a free, web-based logging software designed for ham radio enthusiasts. It’s feature-rich and easy to set up on your own server at no cost. Whether you prefer managing your own installation or having someone else handle the technical details, Wavelog offers flexible options:

- **Install on your own server:** You can set up your own Wavelog server by following the installation instructions. This allows you to have full control over your logging software, and it's completely free to do so.
- **Hosted solutions:** If you’d rather not worry about server administration, there are hosting services available at a cost. These services handle everything for you, including LAMP stack administration and regular Wavelog updates, so you can focus on using the software without technical concerns.

### Try Wavelog Before You Commit

If you're new to Wavelog and want to try it out before setting up your own server, you can explore its features on their demo page. Simply visit the [Wavelog demo](https://demo.wavelog.org/user/login) to log in and see how it works in practice. The demo gives you a great feel for what Wavelog can do and whether it suits your needs.

Whether you choose to run your own installation or use a hosting service, Wavelog is a powerful and versatile tool for logging and managing your ham radio contacts.

## Important Notice: Required Wavelog Features

To ensure the **Wave-Flex Integrator** works properly, two key features from Wavelog must be in place. As of now, these features are only available in Wavelog’s development (`dev`) branch. If you set up your own Wavelog server, you will need to switch to this branch to access them. However, if you use a hosted Wavelog server, you should ask the server administrator if they have implemented the "log_qso" API yet. It's because that is a key feature that is quite new and it's not sure that they have applied that yet.

### Important Disclaimer

Please be aware that using the `dev` branch means you are working with code that is under active development. This branch may include experimental features, incomplete functionality, or potential bugs that have not yet been thoroughly tested. By switching to the Wavelog `dev` branch:

- **You accept the risks** that come with using a development version of the software.
- **The responsibility for any issues** arising from the use of the `dev` branch lies with the user.
- **The Wavelog team and the Wave-Flex Integrator project** cannot guarantee support or stability when using the `dev` branch.

Proceed with caution, and make sure you understand how to switch back to the stable version if necessary.

### How to Switch to the Wavelog dev Branch

Follow these steps to update your Wavelog installation on the Wavelog server to the latest `dev` branch. Please note, in some cases, these steps may vary depending on your setup or any customizations you may have:

   ```bash
   cd /var/www/wavelog # Replace path with your installation folder if necessary
   git fetch # Fetch the latest updates from the Wavelog repository
   git checkout dev # Fetch the latest updates from the Wavelog repository
   git pull origin dev # Pull the latest changes to ensure your Wavelog is up-to-date:
   ```

## Prerequisites for Windows Installation

Before installing, ensure the general [requirements](#requirements) and additionaly that:

- **Node.js**: Download and install the latest version of Node.js [here](https://nodejs.org/). The application requires at least version 12.
- **NPM**: Installed automatically with Node.js. Verify your version using `npm -v` and update it if necessary by running `npm install -g npm`.
- **Git**: Install Git for version control and repository cloning from [here](https://git-scm.com/).

## Installation

### Windows NPM Installation

```bash
git clone https://github.com/tnxqso/wave-flex-integrator.git
cd wave-flex-integrator
npm install
npm start
```

For other platforms like macOS or Linux, or if you prefer to use a binary, we will provide specific instructions soon.

## Configuration

Upon first startup, you will need to configure the application via the **Configuration Tab**. The details you input will be saved automatically using Electron JSON storage. Here are the fields you need to configure:

### Configuration Parameters

- **DX Cluster Settings**:
  - `Host`: The hostname or IP address of your DX Cluster server.
  - `Port`: The port number of your DX Cluster server.
  - `Callsign`: Your amateur radio callsign used for login.
  - `Login Prompt`: The login prompt format for your DX Cluster (optional).
  - `Commands After Login`: Commands you want the system to send after successfully logging in (optional).
  - `Reconnect Settings`: Configure reconnection behavior with initial delay, max delay, and backoff factor.
 
> **Tip:** If you plan to use a DX Cluster server other than the default (dxc.mx0nca.uk on port 7373 is a good alternative for Europe), it is highly recommended that you first connect to the DX Cluster using a Telnet client like [Putty](https://www.putty.org/). This allows you to verify that the login prompt matches your configured settings and that any custom commands will work without errors. There are many DX Clusters available, so if needed, search the internet for alternatives.

- **FlexRadio Settings**:
  - `Enabled`: Enable or disable FlexRadio integration.
  - `Host`: The hostname or IP address of your FlexRadio device. It must be reachable at that hostname or IP from your desktop computer where Flex-Wave Integrator is running.
  - `Port`: The port number to connect to FlexRadio.
  - `Spot Management`: Customize how long spots remain active and their display colors.

> **Tip:** Coloring the spots sometimes gives other results than expected when shown on the SmartSDR panadapter. Use the default colors to start with and change only a single color at a time.

- **Wavelog Settings**:
  - `BASE URL`: The base URL for your Wavelog API, e.g. `https://YOURSERVERNAME/index.php`. Keep the /index.php at the end unless you have <a target="_new" href="https://github.com/wavelog/Wavelog/wiki/Wavelog.php-Configuration-File">modified Wavelogs .htaccess file using mod_rewrite</a>)
  - `API Key`: Your Wavelog API key. You can generate one by clicking your account at top right corner --> API Keys
  - `Station Location IDs`: A comma-separated list of station location IDs (optional). If you don't want the API to search all your station locations defined in Wavelog, otherwise leave blank.

- **Logging Settings**:
  - `Level`: Set the logging level (error, warn, info, debug).
  - `Debug Mode`: Enable or disable debug logging. Warning, debug mode is very verbose.

## Usage

Simply run the application after configuring it:

```bash
npm start
```

For binary installations, details will be provided soon.


## Upgrading Wave-Flex Integrator

1. Open a command prompt window.
2. Change to the directory where Wave-Flex Integrator is installed, e.g.:
   ```bash
   cd wave-flex-integrator
   ```
   
   Make sure that went well before you continue to next step.

3. Pull the latest changes from the repository:
   ```bash
   git reset --hard 
   git pull origin main
   ```


This ensures your local repository is now an exact match with the remote Wave-Flex Integrator branch.


## Contributing

Contributions are welcome! If you have skills in JavaScript, Node.js, or amateur radio integration, feel free to open an issue or submit a pull request on GitHub. Help us enhance features, fix bugs, and grow this project.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

Interested in enhancing your FlexRadio experience? Become a beta tester or contributor! Learn more about the project and join the discussion at [FlexRadio Community](https://community.flexradio.com/discussion/comment/20613338).

## Acknowledgments

- [FlexRadio Systems](https://www.flexradio.com/)
- [Wavelog Logging Software](https://www.wavelog.org)
- [DX Cluster Networks](http://www.dxcluster.info/)
- Thanks to all contributors and the amateur radio community for their support.
