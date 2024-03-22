# KSL macOS installation guide

> [!NOTE]  
> The installation process will be shown using CarX as an example. The process is the same for all Unity games with **mono** runtime.

## 1. Download latest KSL release

Go to [**releases**](https://github.com/trbflxr/ksl/releases) and download the latest KSL release.

> [!IMPORTANT]  
> Keep in mind that for **macOS** you have to download the archive with **osx** suffix.

![latest_release](../images/install_release_osx.png)

## 2. Open the game folder

![open_folder](../images/install_open_folder.png)

## 3. Extract the downloaded archive and drag its contents to the application folder

![drag_files](../images/install_drag_osx.png)

Replace all the files if needed.

![replace_files](../images/install_replace_osx.png)

## 4. Open the run_ksx.sh file in a text editor

![edit_sh](../images/install_open_sh_osx.png)

## 5. Edit the run_ksx.sh file

Edit **only** this line to include the game .app name.
In this example: "CarX Drift Racing Online.app"

![edit_sh](../images/install_edit_sh_osx.png)

Save the file and close the editor.

## 6. Update the run_ksx.sh file permissions

First copy the application folder path. To do it use <kbd>Option</kbd> + <kbd>Command</kbd> + <kbd>C</kbd> combination.

Open spotlight search using <kbd>Command</kbd> + <kbd>Space</kbd> and type "terminal" in it.

![terminal_open](../images/install_terminal_open_osx.png)

Type ```cd "<Paste the path from clipboard here>"``` and press <kbd>Return</kbd>.

![terminal_cd](../images/install_terminal_cd_osx.png)

Type ```chmod +x run_ksl.sh``` and press <kbd>Return</kbd>. It will add execute permission to the script.

## Installation completed

From this point you can start the game from the terminal with KSL enabled and from steam to play without the mods.

But there is an optional step to start the game with mods from steam.

Select the run_ksx.sh file and press <kbd>Option</kbd> + <kbd>Command</kbd> + <kbd>C</kbd> to copy it's path.

![sh_path_copy](../images/install_select_sh_osx.png)

Open application properties

![app_props](../images/install_app_props.png)

Add a launch option for the game. First open double quotes and paste the path you copied in it. Then add space and ```%command%```.
It should look like this ```"/Users/trbflxr/Work/carx/run_ksl.sh" %command%```

Done. Now you can launch the game with KSL enabled from the steam application.
