# ttconnect
Currently just a draft file of a convenience script for connecting to TPU-v4 VMs using tmux. 


## Installation
```bash
# You might have to put "sudo" in front
# Download ttconnect to any directory in your path where you have write access (like /usr/local/bin)
wget 

# Make the program executable
chmod +x /usr/local/bin/ttconnect
```

## Use
While the script also works on a single TPU slice, its main purpose is when working with the pods. It queries gcloud to figure out the number of TPU slices, and then opens a tmux window with a tile for each of the TPU slices. The general layout will be one tile to the left, and the rest of the tiles to the right. It then sets the _syncronize-panes_ parameters so that you can perform the same actions in all the panes. This can however easily be turned off to be able to control the slices individually.

```bash
# Open a connection to a already existing TPU VM or TPU-pod VM
ttconnect MyTPU

````



