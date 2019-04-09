# Powerline for MacOS


- this is a mash up of a few guides.

###  Install Python 
Because Powerline is a Python app, we need to have Python and that too a proper version of Python.

- MacOS comes with Python installed already. Ensure Python’s version is 2.7.x by typing `python -V` in the Terminal.
- If it’s not 2.7, install  [Homebrew](https://brew.sh/)  that allows us to install various software from the CLI, by running:
`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
- Run `brew install python`  to install the latest Python via Homebrew

### Install pip
Install pip, a package manager for Python (similar to NPM)
Install pip by running the following command:
`sudo easy_install pip`

### Install Xcode
- install Xcode from App Store and open Xcode at least once.

### Install Powerline
- Finally, install the Powerline (stable version) via pip by running the following command : `pip install --user powerline-status`


### Add the Powerline daemon to bash
We now need to add the Powerline daemon to bash so that it can monitor the Terminal prompt and make changes

- Copy the Powerline’s installation location:
`pip show powerline-status`
Copy the value from the `Location` field.

We must add the daemon with a proper location to .bash_profile:
	- Make sure you have `.bash_profile` file in your root directory. If not following create one by doing:`cd ~ && touch ~/.bash_profile`
	- Open `.bash_profile` and add the following:

::.bash_profile::
```bash
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
export PATH=$PATH:$HOME/Library/Python/2.7/bin
powerline-daemon -q
POWERLINE_BASH_CONTINUATION=1
POWERLINE_BASH_SELECT=1

# adjust this location with the one you copied earlier
. /Users/rupa/Library/Python/2.7/lib/python/site-packages/powerline/bindings/bash/powerline.sh
```

- Restart the Terminal

----

### Installing fonts
- use these commands
```bash
# clone font repo:
git clone https://github.com/powerline/fonts.git --depth=1

# install fonts:
cd fonts
./install.sh

# clean-up a bit:
cd ..
rm -rf fonts
```

- To use the correct font in VS Code, add following line to user settings:
```json
"terminal.integrated.fontFamily": "'inconsolata for powerline'",
```
- you may need to add the font to your chosen terminal app also.


### Adding Git Status segment

- `pip install --user powerline-gitstatus`

- Again find your Powerline install location with
`pip show powerline-status`

- got to your Powerline install dir and edit the `default.json`  in following sub dir :
`/powerline/config_files/colorschemes/default.json`

- Add following lines:
```json
"gitstatus":                 { "fg": "gray8",           "bg": "gray2", "attrs": [] },
"gitstatus_branch":          { "fg": "gray8",           "bg": "gray2", "attrs": [] },
"gitstatus_branch_clean":    { "fg": "green",           "bg": "gray2", "attrs": [] },
"gitstatus_branch_dirty":    { "fg": "gray8",           "bg": "gray2", "attrs": [] },
"gitstatus_branch_detached": { "fg": "mediumpurple",    "bg": "gray2", "attrs": [] },
"gitstatus_tag":             { "fg": "darkcyan",        "bg": "gray2", "attrs": [] },
"gitstatus_behind":          { "fg": "gray10",          "bg": "gray2", "attrs": [] },
"gitstatus_ahead":           { "fg": "gray10",          "bg": "gray2", "attrs": [] },
"gitstatus_staged":          { "fg": "green",           "bg": "gray2", "attrs": [] },
"gitstatus_unmerged":        { "fg": "brightred",       "bg": "gray2", "attrs": [] },
"gitstatus_changed":         { "fg": "mediumorange",    "bg": "gray2", "attrs": [] },
"gitstatus_untracked":       { "fg": "brightestorange", "bg": "gray2", "attrs": [] },
"gitstatus_stashed":         { "fg": "darkblue",        "bg": "gray2", "attrs": [] },
"gitstatus:divider":         { "fg": "gray8",           "bg": "gray2", "attrs": [] }
```


- lets add the actual git-status segment in the file:
`/powerline/config_files/themes/shell/default.json`

- Then, add the following code to the `left` segment:
```json
{
    "function": "powerline_gitstatus.gitstatus",
    "priority": 40
}
```

- reset powerline:
- `powerline-daemon —replace`
- all should now work!

