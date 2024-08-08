# SLURM commands plus

SlURM is great, but there is a lot of things that annoy me about it. Contained
is a collection of scripts that you can add to your path that may be of use
to you.

## slurmScript

Run this to create the basic structure of a slurm script, hassle free.

Long gone are the days of looking through old scripts, copying the top, 
pasting, then changing individual lines.

Fuck that noise. Just make a script to do it for you.

## bacct (a better sacct)

How often do you find yourself using `sacct` over and over and over and over 
and over again whilst waiting for a job to exit the pending/running stage?

Well, now you don't have to. Just use:

```bash
bacct [iterations=10]
```

and `sacct` will run the number of times you tell it to with 10 second sleeps. 

Hooray!

## getNode

Sometimes a script is running on a node that you don't want it to. In the past
some nodes are down or have a full `/tmp` directory and yet scripts still run
on them. SLURM doesn't tell you which node is being used for a script unless
you start digging a little. This script will help you to detect these problems
earlier.
