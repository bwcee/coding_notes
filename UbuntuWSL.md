# Ubuntu on WSL

1. to access home directory from windows explorer `\\wsl$`

2. in ubuntu terminal first `cd ~` which will bring me to home for ubuntu... then `explorer.exe .` which will open up windows explorer at home for ubuntu

3. [Nodemon and webpack-dev-server hot reload not working under WSL 2 after Windows 10 resinstall](https://stackoverflow.com/questions/62780245/nodemon-and-webpack-dev-server-hot-reload-not-working-under-wsl-2-after-windows)

> I figured this out on my own. Just posting it here in case somebody encounters the same issue. The difference between my system now and before the re-installation is that I upgraded to WSL2. For some reason nodemon and webpack-dev-server hot reload does not work in WSL2. Downgrading to WSL 1 resolved the issue.

> EDIT: In order for this to work in WSL 2, the project needs to be inside the linux file system. (I figured it out a long time ago, just forgot to post it here.)

4. [Set Linux Distro Version to WSL 1 or WSL 2 in Windows 10](https://winaero.com/set-linux-distro-version-to-wsl-1-or-wsl-2-in-windows-10/)
   `wsl -l -v`
   `wsl --set-version Ubuntu 2`

5. [How do I see what packages are installed on Ubuntu Linux?](https://www.cyberciti.biz/faq/apt-get-list-packages-are-installed-on-ubuntu-linux/)

# Reinstalling Ubuntu on WSL

### To change wsl distro, run the following commands in Windows Powershell... pref as admin... not sure if it wld work otherwise...

1. check out the list of [basic wsl commands](https://docs.microsoft.com/en-us/windows/wsl/basic-commands)

2. from the ref above, may want to update to latest version of WSL linux kernel `wsl --update`

3. prefer to also set default WSL version to 1 `wsl --set-default-version <Version>`

4. unregister old version of distro `wsl --unregister <DistributionName>` to uninstall. this shld wipe selected distro including all previously installed apps... i.e. shld be clean slate to start over...

5. `wsl --list --online` to see a list of available distros and run `wsl --install -d <DistroName>`, in my case `wsl --install -d Ubuntu` to [install a distro](https://docs.microsoft.com/en-us/windows/wsl/install#install)

### After Ubuntu installed, can use Windows Terminal window tt opens up Ubuntu terminal

1. follow instructions frm [rocket](https://bootcamp.rocketacademy.co/course-logistics/required-hardware-and-software) to ensure Ubuntu has necessary updates/ installations... `sudo apt update`, `sudo apt upgrade`, `sudo apt install build-essential`, `sudo apt-get install ca-certificates`

1. `lsb_release -a` to chk version of Ubuntu installed

1. to see what has been installed on Ubuntu, run `apt list --installed`

1. follow instructions [here](https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-wsl) to install Node.js in Ubuntu together w nvm

1. to put bck alias to shorten command prompt path... see here on [creating a .bash_aliases file](https://www.cyberciti.biz/faq/create-permanent-bash-alias-linux-unix/) to store aliases and here on the command for a [shortened command prompt](https://bashrcgenerator.com/)

1. to edit bash*aliases file in vscode, use `code ~/.bash_aliases`, `cd /mnt/c/Users/boon*/Desktop/rocketacademy/bootcamp`and`PS1="\[\033[38;5;87m\]>\[$(tput sgr0)\]"`

1. reinstall postgresql with rocket instructions [here](https://bootcamp.rocketacademy.co/3-backend-applications/3.4-sql-applications/3.4.1-postgresql-psql) note instructions disabled requirement for password to access databases

1. [Run Multiple Instances of Same Linux Distro on WSL (Windows 10/11)](https://sungkim11.medium.com/why-you-should-use-multiple-instances-of-same-linux-distro-on-wsl-windows-10-f6f140f8ed88)

1. To install different distros on WSL, just `wsl --install -d <DistroName>`, to switch between the distros, just `wsl -d <DistroName>`

### Windows Terminal

1. [windows terminal docs](https://docs.microsoft.com/en-us/windows/terminal/)
