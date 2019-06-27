## i3 Configuration Creator

This was created in an effort to allow the better organization of an i3 config
file. Currently there is no way to include extra files in the main
`~/.i3/config` file.

Here is an example of how your i3 config can look by using this script:
https://github.com/kenyonj/dotfiles-legacy/tree/99ce9a5dd79191e6699575b9b64f8302d785f780/tag-i3/i3/config.d

### Usage

Create a new directory in your `~/.i3` directory called `config.d`. In this
directory you will need a configs import file. This script assumes that the
imports file is named `i3_configs.conf`, create it with the contents following
this pattern:

`# ~/.i3/config.d/i3_configs.conf`

```bash
# the vars file needs to be first so that other config files can use the vars
# defined within it.
import vars.conf;

import base.conf;
import colors.conf;
import gaps.conf;
import menus.conf;
import screenshots.conf;
import terminal.conf;
import todo.conf;
import containers.conf;
import workspaces.conf;
import xf86.conf;
```

Each one of the above referenced files will be located in the `config.d`
directory and will be formatted the same as your current i3 config file. This
way you can separate the configuration options for different parts of your i3
configuration and feel a little more organized.

Once you have this structure setup, you can execute `create_config` and it will
delete your current `~/.i3/config` file and create a new one using the files
that in your `i3_configs.conf` file.

### Tips

Execute the `create_config` script in these places so that you are always using
your latest edits:

`~/.xinitrc`

```bash
# load Xresources
xrdb -load ~/.Xresources &
xrdb -merge ~/.Xresources

#load xmodmap
xmodmap ~/.Xmodmap

#create i3 config
~/.i3/create_config

#start i3
exec i3
```

`~/.i3/config.d/base.conf`

```bash
# i3 shorcuts for reload/restart
bindsym $mod+$other+Shift+C exec ~/.i3/create_config reload
bindsym $mod+$other+Shift+R exec ~/.i3/create_config restart
```
