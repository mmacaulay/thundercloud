## ThunderCloud installation files

This repository hosts the installation files used by a Chrome extension called _ThunderCloud_. ThunderCloud makes your iCloud tabs available directly in Google Chrome. You can download ThunderCloud from [The Chrome Webstore](https://chrome.google.com/webstore/detail/kdjbkjcmgedoelefbopcifaffcdbehlc/).

I've made these files available on GitHub so anyone can check them and see that they're completely safe and won't do anything they shouldn't. This readme will include an explanation why these files are needed and what they do.

Your iCloud tabs are saved in a file on your Mac, _~/Library/SyncedPreferences/com.apple.Safari.plist_. Chrome Extensions are not allowed to open and read local files. In order for ThunderCloud to have access to your iCloud tabs, the file containing your iCloud tabs needs to be inside the same directory as the files of the extension.

The install file you have to run before you can use ThunderCloud will place a LaunchAgent file inside _ ~/Library/LaunchAgents/_ and load it up with _launchctl_ to make it run every 3 minutes. This task will copy the _com.apple.Safari.plist_ file to the ThunderCloud directory, and convert it into a file that can be read and parsed by ThunderCloud.

### Structure of the repo
Because the version of a Chrome extension is part of the path of its directory, a slightly altered installation file (which points to the new extension path) is needed with every new verion of the ThunderCloud chrome extension. The structure of this directory is based on that fact; every version of the extension gets its own folder. Below is a list of all files inside every directory and a short description of what they'll do.

- **install**; this file includes all the commands to place a LauchAgent file on your Mac and load it up in _launchctl_. It will be loaded by the user using a _curl_ command.

- **com.jeffreywashere.thundercloud.xml**; this is the LaunchAgent file that gets placed on your Mac. Note that this file is hosted as a XML file. During the installation process, it'll get saved as a plist file.

- **uninstall**; this is basically the opposite of the **install** file. It includes all commands to unload and delete the LaunchAgent file.

- **update**; this will unload and delete the LaunchAgent file belonging to an older version of ThunderCloud, and install the new one. _(Note that this is not necessarily for version 1.0 since it's the first version, and will only be included in later versions.)_