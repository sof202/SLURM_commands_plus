# SLURM commands plus

SlURM is great, but there is a lot of things that it doesn't do that pisses me
off. Contained is a collection of scripts that you can add to your `$PATH` that
may be of use to you.

You may find it useful to create a symlink to these scripts if you don't want
to add anything to your `$PATH`. You can do this with:

```bash
ln -s path/to/this/repo/script-name path/to/somewhere/on/$PATH/
```

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
