#

---

# Automating Linux Package Installation

---

## Overview
alpi automates the installation of a predefined list of packages on your system.

It is designed to make setting up a new environment or system easier by quickly installing essential software packages with a single command.

It provides various features including package installation, maintenance, health checks, configuration management, and more, all through a flexible command-line interface.

---
## Table of Contents
* [Prerequisites](#prerequisites)
* [Features](#features)
* [Installation Instructions](#installation-instructions)
* [Usage](#usage)
  * [Manager Options](#manager-options)
  * [Available Options](#available-options)
  * [Examples](#examples)
* [Configuration](#configuration)
  * [Default Configuration](#default-configuration)
  * [Custom Configuration](#custom-configuration)
* [Logging](#logging)
* [License](#license)
* [Troubleshooting](#troubleshooting)
* [Supported Operating Systems](#supported-operating-systems)
* [Contributing](#contributing)
* [Conclusion](#conclusion)

---

## Prerequisites
- A Unix-based operating system (Linux or macOS).
- **Root privileges** may be required to install packages and perform maintenance.
- Package manager must be installed and configured on your system (`apt`, `dnf`, `pacman`, etc.).
- A list of packages should be in the file `alpiList` local or remote (one package per line).

## Features
* **Package Management**: Easily install, remove, or check the status of packages on your system.
* **Maintenance**: Perform system package maintenance tasks like updating, upgrading, and fixing broken packages.
* **Health Checks**: Run diagnostics to ensure your system is up-to-date.
* **Configuration Management**: Support for custom configuration files for package installation and script behavior.
* **Logging**: All actions performed by the script are logged for future reference.

---

## Installation Instructions
> Download and Execute.
   ```bash
   curl -O https://gitlab.com/ibnqhader/alpi/-/raw/main/installer
   ```
   ```bash
   chmod +x installer
   ```
   ```bash
   ./installer
   ```
The installer will install the application manager. which can be used to manage and maintain the app up-to-date.

> Install the application
   ```bash
   alpim install
   ```
Manager will install and configur the application.

## Usage

### Manager options
| Option       | Description                                            |
| ------------ | ------------------------------------------------------ |
| `install`    | Installs the app.                                      |
| `update`     | Checks for updates and installs the new version.       |
| `remove`     | Removes the app.                                       |
| `force`      | Removes the complete app directory (use with caution). |
| `version`    | Shows the currently installed version.                 |

---

Once installed you can run the help command to see the available options.
   ```bash
   alpi -h
   ```
### Available Options

| Option                              | Description                                                                                                                               |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `-m`, `--maintain`                  | Run package manager maintenance tasks.                                                                                                    |
| `-a`, `--availability`              | Check the availability of packages.                                                                                                       |
| `-i`, `--installed`                 | Check if packages are already installed.                                                                                                  |
| `-d`, `--dry-run`                   | Perform a dry-run (simulates actions without actually performing any installations, removals, or updates).                                |
| `-H`, `--health-check`              | Perform a system health check. This includes updating and upgrading packages, checking disk space, and fixing broken packages.            |
| `-I`, `--install`                   | Install the packages listed in the local or remote package files. If no file is specified, the default package file (`alpiList`) is used. |
| `-r`, `--remove`                    | Remove and purge the specified packages.                                                                                                  |
| `-c`, `--post-clean`                | Clean up unnecessary packages after installation.                                                                                         |
| `-f`, `--files` <file1> <file2> ... | Specify custom package files to install. You can sepcify the URL of a remote files directly or inside package list files.                 |
| `-C`, `--configure` <file>          | Use a custom configuration file (default: `alpiConf`).                                                                                    |
| `-v`, `--verbose`                   | Display detailed on the configuration environment.                                                                                        |
| `-L`, `--license`                   | Show license information for the script.                                                                                                  |

> **Note**: You need to explicetly specify flags when using multiple flags.

---

### Examples

- **Install packages from the default file**:

   ```bash
   alpi
   ```

- **Run maintenance tasks**:

   ```bash
   alpi -m
   ```

- **Check availability of packages**:

   ```bash
   alpi -a
   ```

- **Dry run the installation** (simulates the installation process):

   ```bash
   alpi -d
   ```

- **Perform a health check** (update, upgrade, and fix broken packages):

   ```bash
   alpi -H
   ```

- **Install packages from a custom file**:

   ```bash
   alpi -I -f https://gitlab.com/ibnqhader/alpi/-/raw/main/pkg/alpiList packageList.txt
   ```

- **Remove specified packages**:

   ```bash
   alpi -r -f <URL path> and/or <file path>
   ```

---

## Configuration

### Default Configuration

By default, the script uses the following files and settings:

* **Package File**: `alpiList`
  The script will read package names from this file, one per line. If no file is specified, this file will be used.

* **Configuration File**: `alpiConf`
  The script uses this file to configure its environment. You can override these setting using the `-C` option.

* **Log File**: `alpiLog`
  Logs for all script actions are written to this file. You can review it for debugging or record-keeping.

### Custom Configuration

You can create a custom configuration file for your needs. The configuration file should contain key-value pairs to define environment variables, package lists, or other settings that the script will use.

Example configuration:

```bash
DEFAULT_PACKAGE_FILE="<File Path>"
LOG_FILE="<File Path>"
LOCK_FILE="<File Path>"
```

---

## Logging

All actions performed by the app are logged for accountability and debugging purposes. The default log file is defined by the `$LOG_FILE` variable, but you can customize it.

* **Log Format**: Each log entry includes the action taken, and any relevant output or errors.

* **Location**: The default location for logs is `$LOG_FILE`. To specify a custom log file, use the `-v` option, and modify the `$LOG_FILE` in the configuration.

---

## License

This script is distributed under the [GNU AGPL V3](https://www.gnu.org/licenses). You can view the full license information by running the script with the `-L` flag.

---

## Troubleshooting

If you encounter issues while running the script, here are some common solutions:

* **Permissions Issues**

  * Ensure you have the necessary privileges to perform package management tasks. Use `sudo` if required.

```bash
sudo alpi
```

* **Missing Dependencies**

  * If you see errors related to missing dependencies, make sure your package manager is set up correctly, and the package names are valid.

* **File Not Found Errors**

  * Ensure that your package list file and configuration file paths are correct. You can verify the paths by checking the environment variables `-v` or using the `-f` and `-C` options.

* **Log Review**

  * Review the logs in `alpiLog` to check for any specific error messages or warnings that could help diagnose the issue.

---

## Supported Operating Systems

* Linux (Ubuntu/Debian, CentOS/Fedora, Arch, etc).
* macOS (with Homebrew).
* Unix based Systems.

---

## Contributing

If you find any issues or have suggestions for improvements, feel free to open an issue or discuss in wiki, submit a pull request.

---

## Conclusion

alpi is a powerful tool to manage your system’s package installation, maintenance, and configuration. With a variety of features, it helps automate and streamline the process, making it easier to manage your environment with minimal manual intervention.

---
