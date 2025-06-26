# scancel-last

**Cancel your most recent SLURM jobs safely and efficiently.**

A lightweight and safe Bash utility to cancel the **last _N_ jobs** you submitted to a SLURM-managed HPC cluster.Sometimes, especially when submitting jobs in bulk, something goes wrong — a wrong input file, incorrect script, or parameter error. Instead of canceling each job manually, `scancel-last` helps you terminate your most recent jobs in a controlled, transparent way.

## Features

- Cancels the **last N jobs** submitted by the current user, in **reverse order** (newest first)
- Displays job information and  requests confirmation before proceeding

## Installation

Download the package using

```
git clone https://github.com/jgrll/scancel-last.git ~/scancel-last
```

Move to the destination folder and execute ./install to add the path to your .bashrc file and voilà!

---

## Usage

```
scancel-tail <number_of_jobs_to_kill>
```

---

## Example

Suppose you've submitted a batch of 22 jobs but realize that the last 20 were misconfigured.

You check your jobs with

```
squeue -u $USER
```

Output:

```
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
           1234567     cpu01     test     jdoe  R       0:10      1 node01
           1234568     cpu01     test     jdoe  R       0:09      1 node01
           1234569     cpu01     test     jdoe  R       0:01      1 node02
           1234570     cpu01     test     jdoe PD       0:00      1 (Priority)
           ...
           1234586     cpu01     test     jdoe PD       0:00      1 (Priority)
```

You want to keep jobs 1234567 and 1234568 and cancel the last 20:

```
scancel-last.sh 20
```

Output:

```
The most recent 20 job(s) to be canceled:
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
           1234569     cpu01     test     jdoe  R       0:01      1 node02
           1234570     cpu01     test     jdoe PD       0:00      1 (Priority)
           ...
           1234586     cpu01     test     jdoe PD       0:00      1 (Priority)        
Are you sure you want to kill these 20 job(s)? [y/N] y
Killing job 1234569...
...
Killing job 1234586...
Successfully canceled the most recent 20 job(s).
```

---

## Licence

This project is licensed under the MIT License.

---

## Author

[jgrll](https://github.com/jgrll)

Feel free to open an issue or pull request if you have suggestions or encounter a bug.


