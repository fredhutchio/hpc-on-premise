## Environments

Your compute environment is the collection of machinery, software, and networks on which you perform tasks. Managing environments is challenging, but there are tools available to help you stay on the right track.

### Finding and loading software

Rhino has hundreds of pieces of software installed, so it uses a module system to make software available for use. To see what software you currently have loaded:

    module list

If you're looking for a specific package, you can search using terms related to the name of the software:

    module avail seq

If you see the package you want, you can load it with:

    module load seqtools

...or the abbreviated version, which is the same as above:

    ml seqtools

Be careful with multiple versions of the same software! You can load specific versions too:

    ml seqtools/4.29

### Conda to control environments

An alternative method for managing environments is `conda`. You have used this on your own computer by installing Anaconda for our Python exercises, and there are methods for working in Anaconda Navigator to [manage environments](https://docs.anaconda.com/anaconda/navigator/tutorials/manage-environments/).

We can also use `conda` on the command line, even in rhino:

    module spider conda

Note that this a method for running Python, too! We can now double check our version:

    conda --version

You can use `conda` to create named environments that will allow you to maintain specific software versions for different projects. For more information on managing `conda` locally, go [here](https://docs.conda.io/projects/conda/en/latest/user-guide/getting-started.html).

### Setting your path

Let's clear out our loaded modules to make the next section easier to manage:

    module purge

What is in your path? This indicates where your computer will look for executable software:

    echo $PATH

Make a directory to hold the software you want to install (this could be a GitHub repo that contains the scripts you use commonly):

    mkdir ~/my_scripts

Add that location to your path so it is search automatically for executable programs:

    export PATH=$PATH:~/my_scripts

Now you'll see your `my_scripts` folder listed, so that your scripts will automatically be searched when you try to run a command. For more information, see [adding a path to your path](https://opensource.com/article/17/6/set-path-linux).

### Environment variables

The things that start with a `$` in the explanations above represent [environment variables](https://opensource.com/article/19/8/what-are-environment-variables), or information about your session that is used as you execute commands. We can view all environmental variables with:

    env

If we load a new module and then rerun that:

    ml fastqc
    env

...we'll now see FastQC included in our environmental variables.

Note that we can also set our own variables in shell scripts!