## Running software

We talked briefly about viewing and managing processes in our last class. Look [here](https://www.guru99.com/managing-processes-in-linux.html) for more information about these commands:

    ps
    top
    kill

When working on a shared compute cluster, though, we'll need to be a bit more careful about how we run programs (especially large jobs).

### Running jobs interactively

When you log on to the cluster, all commands you run are limited by the compute resources associated with your default login (and by the cluster being shared by many people!). It's good etiquette, and often a necessity, to request your own node for additional tasks:

    grabnode

When prompted, you should type 1 for number of CPUs (since there are lots of us in this class!), hit `Enter` to select the default for memory, and type 1 for number of days. You'll note your command prompt will switch to say `gizmo` instead of `rhino`; you can interact with your directories the same as you would normally. See [this documentation](https://sciwiki.fredhutch.org/compdemos/howtoRhino/#guidance-for-use) for more information on when to use `grabnode`. To end your session on `gizmo`:

    exit

This will take you back to your tumor `rhino` login prompt.

### Cluster job submission

In some cases, you may not want to run jobs manually, and will want to use batch computing. In this approach, you specify the parameters for how a job will be run in a script that will then go into a queue. The batch management system on rhino is called [Slurm](http://schedmd.com/). For more information on using slurm on rhino, go [here](https://sciwiki.fredhutch.org/scicomputing/compute_jobs/#using-slurm-on-fred-hutch-systems).