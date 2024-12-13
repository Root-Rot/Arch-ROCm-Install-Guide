﻿Arch ROCm Guide
Verified working On my RX 6700 XT

1. Update your system with the bellow command: 

sudo pacman -Syu

2. Install a AUR helper of your choice, here we are using yay. Install it with the below command:

sudo pacman -S --needed git base-devel && git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si

3. Install prerequisites with the bellow command:

yay -S wget make curl gperftools

4. Install PyEnv with the bellow command:

curl https://pyenv.run | bash

5. After installing PyEnv add these lines to your .bashrc:

nano ~/.bashrc

6. Add these lines at the bottom of your .bashrc:

export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv virtualenv-init -)"

Ctrl+O then press ENTER to save changes.
Ctrl+X to exit after saving changes.

7. Then refresh your shell using the bellow command:

exec $SHELL

8. Next make sure pyenv is installed by running the bellow command:

pyenv

If it prints a list of commands it is installed and working properly:

9. Install Python 3.10.13 with the bellow command:

pyenv install 3.10.13

10. Next we need to tell the system to use this version of python with the bellow command:

pyenv global 3.10.13

11. To ensure we have the correct python version in use run this command:

python --version

This command should return version 3.10.13.

Install ROCm:

yay -S rocm-hip-sdk rocm-opencl-sdk

12. Next add yourself to these groups and replace username with your own username:

sudo gpasswd -a username render
sudo gpasswd -a username video

If your unsure what your username is, run this in the terminal to find out:

whoami

13. Then add these lines to your .bashrc:

nano ~/.bashrc

Add these lines at the bottom of your file, if you have a RX 7000 series card, change 10.3.0 to 11.0.0:

export ROCM_PATH=/opt/rocm
export HSA_OVERRIDE_GFX_VERSION=10.3.0

Ctrl+O then press ENTER to save changes.
Ctrl+X to exit after saving changes.

14. Reboot your system either though the GUI or by running this command in your terminal:

sudo reboot

15. Lastly after reboot, check if ROCm is installed by running this command:

rocminfo

If it returns a wall of info and specs about your GPU, it is installed and working correctly.

If all went well, then congrats you have successfully installed ROCm on your AMD GPU.
