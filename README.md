# ttconnect
A script for combining the power of [tmux](https://github.com/tmux/tmux/wiki) with the TPU VMs. The script currently handles both TPU-v3, TPU-v4 and TPU-v5. 


## Installation
```bash
# Download ttconnect
wget https://raw.githubusercontent.com/peregilk/ttconnect/main/ttconnect

# Make the program executable
chmod a+x ttconnect

# Optionally copy it to a place in your path (like /usr/local/bin/)
```

## Use
While the script also works on a single TPU slice, its main purpose is when working with the pods. It will automatically open a tmux window with a tile for each of the TPU slices, allowing them to be controlled both in parallel and individually.

```bash
# Open a connection to an already existing TPU VM or TPU-VMs.
# If one is not provided, it will default to us-central2-b
./ttconnect TPU-name [zone]

````

This command will open connections to all the workers in a tmux with split panes. A typical workspace for a v4-32 looks like this:

![ttconnect screenshot](./screenshot.png)

The default setting is syncronized panes. Whatever you type in one pane, will then happen in all the panes. However, if you like to make a change only to one of the TPUs, you can turn off this behaviour by setting:

```bash
C-b: setw synchronize-panes off
```
Depending upon how many windows that are open, it might be beneficial to change the layout mode. You can cycle through the five different layout modes with this command:

```bash
C-b <space>
```

For more advanced use, please refer to the [tmux documentation](https://man.openbsd.org/OpenBSD-current/man1/tmux.1).

## Feedback
Feel free to modify the script, and to add features. If you come up with improvements, I will be glad to add them into the script. Please send any comments to [per@capia.no](mailto:per@capia.no).

