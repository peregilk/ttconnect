# ttconnect
Currently just a draft file of a convenience script for connecting to TPU-v4 VMs using tmux. 


## Installation
```bash
# Download ttconnect
wget https://raw.githubusercontent.com/peregilk/ttconnect/main/ttconnect

# Make the program executable
chmod a+x ttconnect

# Optionally copy it to a place in your path (like /usr/local/bin/)
```

## Use
While the script also works on a single TPU slice, its main purpose is when working with the pods. It queries gcloud to figure out the number of TPU slices, and then opens a tmux window with a tile for each of the TPU slices. The general layout will be one tile to the left, and the rest of the tiles to the right. It then sets the _syncronize-panes_ parameters so that you can perform the same actions in all the panes. This can however easily be turned off to be able to control the slices individually.

```bash
# Open a connection to a already existing TPU VM or TPU-pod VM. 
./ttconnect [TPU name]

````

This command will open connections to all the workers in a tmux with split panes. A typical workspace for a v4-32 looks like this:



The default setting is syncronized panes. Whatever you type in any pane, will happen in all the panes. However, if you like, this can be turned off by setting:

```bash
C-b: setw synchronize-panes off
```



