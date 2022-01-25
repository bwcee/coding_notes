# Ubuntu on WSL

1. to access home directory from windows explorer `\\wsl$`

2. [Nodemon and webpack-dev-server hot reload not working under WSL 2 after Windows 10 resinstall](https://stackoverflow.com/questions/62780245/nodemon-and-webpack-dev-server-hot-reload-not-working-under-wsl-2-after-windows)

> I figured this out on my own. Just posting it here in case somebody encounters the same issue. The difference between my system now and before the re-installation is that I upgraded to WSL2. For some reason nodemon and webpack-dev-server hot reload does not work in WSL2. Downgrading to WSL 1 resolved the issue.

> EDIT: In order for this to work in WSL 2, the project needs to be inside the linux file system. (I figured it out a long time ago, just forgot to post it here.)

3. [Set Linux Distro Version to WSL 1 or WSL 2 in Windows 10](https://winaero.com/set-linux-distro-version-to-wsl-1-or-wsl-2-in-windows-10/)
   `wsl -l -v`
   `wsl --set-version Ubuntu 2`
