# SDR-Configs
A simple shell script to switch between SDR++ configs


By specifying a "root" folder on the commandline, we can save various setups for SDR++ -- for example: FM broadcast stations, ham radio bands, the air and marine bands, etc.

I wrote a linux shell-script named “_sdrpp.sh” which allows a simple way to save and manage multiple SDR++ configs. 

**Make a set of config.json files for a new setup**

To create a new set of configs (my method): open your files manager and browse to your SDR++ install directory. Mine is “HOME/.local/sdrpp” [this is where the default config files are saved]

There will be nearly 2 dozen xxxxxx_config.json files....create a new folder (eg; safety_backup) and drag all the configs into it. Now the config folder should have no files. Folders are OK.

Start SDR++ and it will create new “default” config files. Modify whatever settings are needed. Quit the program.

In your files manager (you’re still in the SDR++ folder, yes?), create a new folder. You should be able to use any legal name, but I like to stick to letters and the underscore or hyphen.  (eg: FM, ham_radio, Weather, Air-band)

Highlight all the xxxxxx_config.json files and drag them into the new folder.

**Add the new setup to the script**

I keep all the scripts I write in “HOME/.local/bin”, which is on my system’s command-path.

Open the script (HOME/.local/bin/_sdrpp.sh) in your text editor, and edit the line:  

"FM" | "HAM")  

to look like this: "FM" | "HAM" | "NewFolderName")

Case is Significant!

Save the script and now from a command prompt you can type: 

_sdrpp.sh NewFolderName

and your new set of config files will be used, and kept separate from any others. If ‘NewFolderName’ contains a space, use quotes: “NewFolder Name”

When you're done with a setup and want to use a different one, just quit from SDR++ and re-start with the new.

I like to create desktop-manager shortcuts for each SDR++ setup, for easy switching between configs.

HERE'S THE SCRIPT -- copy-and-paste the text below into a file somewhere on your system's 'path'

```
#!/bin/bash  
# A Simple Shell-Script For Multiple SDR++ Setups
#      no parm: use default configs
#   valid parm: use special configs
# invalid parm: exit with error
# AD9FK -- rlw1138 AT hot mail DOT com

if \[ $# -eq 1 \]; then  
  
  VAR=$1
  case $VAR in

  #add new ones to this line, in quotes and separated with |
  "FM" | "HAM")
    #echo "Parameter: $1 sdrpp --autostart --root \"$HOME/.config/sdrpp/$1\""
    sdrpp --autostart --root "$HOME/.config/sdrpp/$1"
    ;;

  *)
    echo "ERROR -- Parameter: $1 -- Invalid"
    ;;
  esac

else  
  #echo "No parameter provided. sdrpp --autostart --root $HOME/.config/sdrpp"
  sdrpp --autostart --root $HOME/.config/sdrpp
fi

```
