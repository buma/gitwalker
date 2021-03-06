What is this?
-------------------
*gitwalker* is a tool for collecting data from git repositories. It automates
the process of checking out each revision, running some command and logging the
output to a JSON file. Additional commands can be added by writing Python classes.

What can it do?
-------------------
Currently _gitwalker_ supports two built in commands:

 * A LaTeX word count
 * du disk usage command
 * Arbitrary shell commands

Its straightforward to add additional commands - see the file `tools.py`

The included script `gitwalk_plot` uses the
[matplotlib](http://matplotlib.sourceforge.net/index.html) framework to produce
time-series graphs overlaying multiple data files.

Getting It
-------------------
If you have *pip* installed, simply
    pip install gitwalker

Usage
--------------------
To word count a git-tracked LaTeX project across all commits:

    gitwalk --wordcount myfile.tex --out wordcount.json /path/to/project

This will clone the repository at `/path/to/project` to a temporary directory
before checking out each revision and running a word count on the file
myfile.tex in the repository. The results will be output to the file `wordcount.json`

*gitwalker* also supports incremental update of a previously produced log file. To add newly committed revisions,

    gitwalk --update wordcount.json --wordcount myfile.tex /path/to/project

There is an attached script to plot a number of such output files on the same
axes using matplotlib. e.g.

    gitwalk_plot --plot file1.json me red --plot you.json you blue wordcount/wordcount

Will plot the files `file1.json` and `file2.json` on the same axes using the
specified labels and colours. The value will be dug out from the JSON file via
the path format at the end of the command line - in this case `wordcount/wordcount`. One could also run

    gitwalk_plot --plot file1.json me red --plot you.json you blue wordcount/nfigures

to plot the number of LaTeX figures present in each commit.

To run a shell command on each commit,

    gitwalk --shell="ls | wc -l" /path/to/project

Todo
--------------------
* Add git-notes option
