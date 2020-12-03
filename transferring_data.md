### Transferring data

So far, we've used GitHub as a location to store files so we can access them remotely (via `git pull`). This has worked for the small, public files we've been using for class, but this is insufficient for most research projects.

You can use GUI software to transfer data files:
- For transferring data from your computer to a remote storage location, we recommend [Cyberduck](https://sciwiki.fredhutch.org/compdemos/Mountain-CyberDuck/#cyberduck)
- For transferring data among Fred Hutch storage locations, we recommend [Motuz](https://sciwiki.fredhutch.org/scicomputing/store_overview/#data-transfer)

Of course, there are also Unix commands to transfer files, called `scp` (secure copy). More complete instructions can be found [here](https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/), but the most straightforward for our purposes will be to open our shell and transfer a file from our local computer (laptop) to the remote computer (rhino). Navigate to the place on your computer where your chr22 directory is saved (see README of this class for more information) and execute:

    scp chr22.tar USERNAME@rhino:~

Where USERNAME, of course, is your own username, and the filename is accurate as per the file on your computer. The part before the colon (`:`) is the same as the login process to rhino; the part after represents the path to where the file is retained on the cluster. The command above command places the file `setup.sh` in your home directory (`~`) on rhino.

You can copy entire directories by making your command recursive:

    scp -r PATH/TO/DIRECTORY USERNAME@rhino:PATH/TO/RHINO/DIRECTORY

This is especially useful when transferring collections of data files, or entire project directories. You can also use wildcards to specify filenames to transfer.

Reverse the order of the directories to download files from a remote resource:

    scp -r USERNAME@rhino:PATH/TO/RHINO/DIRECTORY PATH/TO/DIRECTORY

If you're downloading files from online, you can use:

    wget URL.to.data.file

This downloads a data file and places it in your current working directory with the same filename as at the end of the URL. If you're trying to download a file in the shell on your local machine and `wget` isn't recognized (this is the case on most Macs), try `curl` instead.

Let's set up a project directory for today's class and try out `wget`:

    mkdir lecture_18
    cd lecture_18
    wget http://genomedata.org/rnaseq-tutorial/practical.tar

#### Working with big data

If you're working with many data files (especially when transferring among computers), it may be useful to collect them together into a single file. If you receive a file ending in tar (sometimes these are known as tarballs), you can expand them into a regular, accessible directory using:

    tar -xvf DIRECTORY_NAME.tar

Let's try this out with our downloaded data file:

    tar -xvf practical.tar

You can list all the resulting files to see what was in the archive. What kind of files are these?

If the file is also compressed, you can uncompress and untar in a single step by adding one more flag:

    tar -xvzf DIRECTORY_NAME.tar.gz

Let's try this on the file we uploaded via `scp`:

    tar -xvf chr22.tar

Make sure the flag and filename match those on your computer!

To create the tarball again, use:

    tar -cvf DIRECTORY_NAME.tar DIRECTORY/

In this command, `DIRECTORY_NAME.tar` is the final output file, which contains the entire contents of `DIRECTORY/`. You can also compress at the same time as tar:

    tar -cvxf DIRECTORY_NAME.tar.gz DIRECTORY/

Please note that `tar` is a notoriously difficult command to remember, resulting in [this classic Unix cartoon](https://xkcd.com/1168/).

You can also use compression algorithms without `tar`. The most common include:

    zip
    gzip
    bgzip

These have their equivalent commands to uncompress as well.

#### Confirming data integrity

We can check to make sure our files downloaded appropriately in a few ways. Let's first try to take a peek at the top of one of our data files:

    head hcc1395_tumor_rep1_r1.fastq.gz

Yikes, that doesn't work so well on compressed files! We don't necessarily want to uncompress all our data files, though, so let's try a different tool:

    zcat hcc1395_tumor_rep1_r1.fastq | head

Piping from `zcat` is a great way to inspect sequence files without having to `gunzip` and then `gzip` again.

Compressing and transferring files can sometimes cause problems, especially if the process is interrupted and files are corrupted. You can use [MD5](http://www.digitizationguidelines.gov/term.php?term=md5checksum) (checksums) to check that the entire file is intact. To check a file against another copy, run the following on both files:

    md5sum FILENAME

This creates a unique set of characters that should be identical between the two copies.