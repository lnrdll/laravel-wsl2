# laravel-wsl2

Bootstrap script to configure a Laravel **development** environment on Windows Systems for Linux. For WSL setup, checkout the [laravel-wsl](https://github.com/rlunardelli/laravel-wsl) repository.

## Setup

### Enable WSL2

Follow the instructions in this [documentation](https://docs.microsoft.com/en-us/windows/wsl/install-win10). Once you get WSL enabled, go ahead and install Debian.

### Bootstrap script

Once your WSL is up and running, download the bootstrap script and run it on your WSL. It will perform the following tasks:

1. Update Linux
2. Install and configure PHP 7.4
3. Install MariaDB
4. Install Redis
5. Install composer and valet
6. Install and configure vim
7. Configure xdebug

**Note**: The boostrap script was tested only on a Debian WSL.

### Docroot

Create a docroot where your code will exist. Since the Windows filesystem can be accessed from the WSL `/mnt/`, create a directory shared between the two spaces and symlinked it from your home directory in WSL.

```
ln -s /mnt/c/Users/<username>/<code_directory> ~/code
```

Run `valet` from within this new directory:

```
valet park
```

### Init Laravel

In WSL, navigate to the your code directory and the run the following:

```
composer create-project --prefer-dist laravel/laravel blog
```

Composer will create a `blog` folder will all the boilerplate. You should be able to access it at: ``http://blog.test``.

### VS Code

To get all the VS Code goodness to work with PHP on your Windows box, you need to download the extension [Remote WSL](https://code.visualstudio.com/remote-tutorials/wsl/run-in-wsl). VS Code will add itself to your `%PATH%`, so from the WSL console you can type `code .` to open VS Code on that folder. If for some reason, VS Code is not in your path, you can modify your `~/.bashrc` and add VS Code to your path. By default, VS Code is installed under `C:\users\{username}\AppData\Local\Programs\Microsoft VS Code`.

Add this line to your path:

```
export PATH=$PATH:/mnt/c/Users/{username}/AppData/Local/Programs/Microsoft VS Code/bin"
```

#### Terminal

In case you need to configure VS Code Shell to use the WSL environment, you'll have to update the user's profile settings.

* `File -> Preferences -> Settings`

Then, you'll change/add the following property:

```
"terminal.integrated.shell.windows": "C:\\Windows\\Sysnative\\bash.exe"
```

## License

This project is licensed under the Apache-2.0 License - see the [LICENSE](LICENSE) file for details
