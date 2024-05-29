# ttconnect
A script for combining the power of [tmux](https://github.com/tmux/tmux/wiki) with the TPU VMs. The script currently handles both TPU-v3, TPU-v4 and TPU-v5. The main idea is to use tmux for executing identical commands on multiple VMs.


## Installation
```bash
# Download ttconnect
wget https://raw.githubusercontent.com/peregilk/ttconnect/main/ttconnect

# Make the program executable
chmod a+x ttconnect

# Optionally copy it to a place in your path (like /usr/local/bin/)
```

## Use and Tips
While the script also works on a single TPU slice, its main purpose is when working with the pods. It will automatically open a tmux window with a tile for each of the TPU slices, allowing them to be controlled both in parallel and individually.

```bash
# Open a connection to an already existing TPU VM or TPU-VMs.
# If one is not provided, it will default to us-central2-b
./ttconnect TPU-name [zone]

````

This command will open connections to all the workers in a tmux with split panes. A typical workspace for a v4-32 looks like this:

![ttconnect screenshot](./screenshot.png)

### Layout
Depending upon how many windows that are open, it might be beneficial to change the layout mode. You can cycle through the five different layout modes with this command:

```bash
C-b <space>
```


### Syncronize off
The default setting is syncronized panes. Whatever you type in one pane, will then happen in all the panes. However, if you like to make a change only to one of the TPUs, you can turn off this behaviour by setting:

```bash
C-b: setw synchronize-panes off
```


### Target Specific Panes
It might happen that one of the tpus dies for some reason, and it might not be the one that is in focus. To target specific panes there are a few tricks that I like to use. Firstly you can always go to another pane using `ctrl-b arrow`. However, in many cases this pane is too small to do real work. Then you can cycle so that the layout model is `main-horisontal`(see above). Then use this command to see the id of each of the panes:
```bash
C-b q
```

When you know the id of the target pane, you can use the command below setting the N=id:

```bash
C-b:swap-pane -t N
```

### Kill window
You can detach from the windows by doing 
```bash
C-b d
```
However, if you really want to zap the entire window, you will have to do:
```bash
C-b: kill-window
```
If you have used venv's when setting up the tpus, restarting the entire session, is not really a big deal.

### Killing Stuck Scripts
In rare cases, some scripts crashes. If you dont want to recreate the TPUs/VMs, this is really useful commands.

```bash
gcloud alpha compute tpus tpu-vm ssh MyName --project=MyProject-11111 --zone=MyZone --worker=all --command="sudo pkill -9 python"
```

In some very rare cases, I have experienced that there still can be stuck programs that prevents the training scripts to restart. This is my last trick:

```bash
gcloud alpha compute tpus tpu-vm ssh MyName --project=MyProject-11111 --zone=MyZone --worker=all --command="ps ax | grep python | grep -v grep | awk '{print \$1}' | xargs -r sudo kill -9"
```

For more advanced use, please refer to the [tmux documentation](https://man.openbsd.org/OpenBSD-current/man1/tmux.1).

### Switch Sessions
This is really just an tmux tips but it seems like a lot of tmux users simply is not aware of its most useful feature. List all sessions:

```bash
C-b s
```

## Feedback
Feel free to modify the script, and to add features. If you come up with improvements, I will be glad to add them into the script. Please send any comments to [per@capia.no](mailto:per@capia.no).

