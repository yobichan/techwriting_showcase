# About this guide

This guide helps you install Git on your Windows work computer with WSL preinstalled.

{% include include_git_target_audience.md %}

{% include include_git_prereqs.md %}

# Installing Git on WSL

The full installation of git requires the following steps.

## Starting WSL

To start git on Windows-based systems, do the following:

1. Press the <kbd>Windows</kbd> key on your keyboard.
1. In the search bar, type **_Ubuntu_**. The Ubuntu app should appear in the results.
   ![](../assets/images/start-menu-ubuntu_wsl.png)
1. Click on the **Ubuntu app**. The WSL terminal should open.
   ![](../assets/images/wsl-show-motd.png)
1. At first login, you are prompted to set up your environment. Provide a username and password for you WSL system.

## Updating your package manager

1. Update your Ubuntu operating system.

   ```console
   sudo apt-get update
   sudo apt-get dist-update

   ```

## Installing git

1. Install git with the following command:
   ```console
   sudo apt-get install git
   ```
1. Wait until the installation finishes. For troubleshooting tips, see Troubleshooting.

## Verifying Git installation

To verify git installation, open your terminal and do the following:

1. Check the installed version of Git:

   ```console
   git --version
   ```

   If Git is installed correctly, this command will display the installed version.

1. Verify Git configuration:

   ```console
   git config --list
   ```

   If Git is installed correctly, this command will display the configured username and email.

   ```console
   user.name=Your Name
   user.email=your.email@example.com
   ```

# Configuring Git after installation

1. Configure the **username** and **email** of git using the following commands, where:

   - `your_name` is your name in the format first name and surname
   - `email` is your corporate email address

   ```console
   git config --global user.name <your_name>
   git config --global user.email <email>
   ```

1. Generate an SSH key with the following command:
   ```console
   ssh-keygen -t ed25519 -b 4096 -C <email>
   ```
   When prompted to enter a file, press enter. Do the same when prompted to enter a passphrase.
1. List the contents of the generated file with the following comand:
   ```console
   cat ~/.ssh/id_rsa.pub
   ```
1. Copy the output of the previous command.
1. In your browser, navigate to the company Github website.

# Reviewing installation process

![](../assets/images/git_install_process.png)

# Troubleshooting Git installation

## Symptom: "git: command not found"

**Cause:** Git is not found on your system

**Resolution:**

1. Verify if git is installed with the following command:

   ```console
   which git
   ```

1. If the above command returns no path, install git.

## Symptom: Permission Denied When Running Git

**Cause:** You might be trying to run git without the right Permission

**Resolution:**

1. Run the `git` command with the sudo prefix:
   ```console
   sudo git
   ```
1. Check file permissions:

   ```console
   ls -l /path/to/repository
   ```

1. Change the file ownership:

   ```console

   sudo chown -R $(whoami) /path/to/repo

   ```

# References

{% include includes_git_references.md%}
