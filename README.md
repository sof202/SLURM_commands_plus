# SLURM commands plus

SLURM is great, but there is a lot of things that it doesn't do that pisses me
off. 

Contained is a collection of scripts that you can add to your `$PATH` that
may be of use to you.

You can have this done for you by running the `setup` script located inside
of the setup directory. Upon running please now execute the command:

```bash
source ~/.bash_profile
```

This is also pasted to the terminal after running `setup`.

## slurmScript

Run this to create the basic structure of a slurm script, hassle free.

Long gone are the days of looking through old scripts, copying the top, 
pasting, then changing individual lines.

Fuck that noise. Just get a script to do it for you.

```bash
slurmScript path/to/new-script.sh
$ Enter max wall time (HH:MM:SS): 01:00:00
$ Enter max memory (xxxG): 2G
$ Enter job name: important-job-name
```

## bacct (a better sacct)

How often do you find yourself using `sacct` over and over and over and over 
and over again whilst waiting for a job to exit the pending/running stage?

Well now you don't have to, with `bacct`. This script will automatically
update the output of sacct every 10 seconds for 10 iterations by default. You
can provide it a different number of iterations with the first positional
argument like so:

```bash
# outputs sacct 20 times
bacct 20
```

Hooray!

## getNode

Sometimes a script is running on a node that you don't want it to. In the past
some nodes are down or have a full `/tmp` directory and yet scripts still run
on them. SLURM doesn't tell you which node is being used for a script unless
you start digging a little. This script will help you to detect these problems
earlier.

`getNode` requires one input for the SLURM job ID, and can give a more verbose
output if supplied with the `-v` option like so:

```bash
# outputs just the node
getNode 123456
$ comp071

# ouputs node in human readable format
getNode -v 123456
$ Job 123456 is running on: comp071
```

## getScriptLocation

When running a shell script directly through `bash` you can obtain the location
of the script very simply with `$0`. Unfortunately with SLURM scripts this is
no longer possible as SLURM creates a copy of your script into 
`/var/spool/slurmd/job[jobID]/slurm_script`.

Allowing a script to know where it is on the file system can be very useful
and helps with portability. If everyone would agree to run scripts from the
directory they are in we could just use `$SLURM_SUBMIT_DIR`. But life isn't
that easy unfortunately. 

Introducing `getScriptLocation`. This script requires one input for the SLURM
job ID, and can give a more verbose output if supplied with the `-v` option
like so:

```bash
# outputs script location
getScriptLocation 123456
$ /path/to/your/script.sh

# ouputs script location in human readable format
getScriptLocation -v 123456
$ script.sh (Job ID: 123456) is located at: /path/to/your/script.sh
```

Furthermore, you may just want to get the directory that the script is located
in. To do this, provide the script with the `-d` option like so:

```bash
# outputs the directory the script is in
getScriptLocation -d 123456
$ /path/to/script/directory

# ouputs the directory the script is in in human readable format
getScriptLocation -vd 123456
$ script.sh (Job ID: 123456) is located at: /path/to/script/directory
```
