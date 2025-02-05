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
