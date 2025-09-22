# Introduction of HPC using Argon

## Accessing Argon

[details](https://uiowa.atlassian.net/wiki/spaces/hpcdocs/pages/76513416/Accessing+HPC+resources)

- On campus or off campus with VPN

    ```bash
    > ssh HawkID@argon.hpc.uiowa.edu
    ```

- Off campus without VPN

    ```bash
    > ssh -p 40 HawkID@argon.hpc.uiowa.edu
    ```

!!! info "The activation of VPN is recommended for security when you access outside campus."


## Evironment modules on Argon
[details](https://uiowa.atlassian.net/wiki/spaces/hpcdocs/pages/76513436/Environment+Modules)

!!! note "module list"

    list currently loaded modules

    ```bash
    dooyoon@argon-itf-login-4 ~> module list

      Currently Loaded Modules:
        1) stack/2021.1
    ```
    
!!! note "module avail [package]"

    search information of the package under the current stack

!!! note "module spider [package]"

    search detailed information of the package in all stacks

!!! note "module load [package]"

    load the module 

!!! note "module unload [package]"

    unload the module

!!! note "module reset"

    set the environment to the default configuration

!!! note "module purge"

    remove all modules 
   


## SGE Jobs
[details: basic submission](https://uiowa.atlassian.net/wiki/spaces/hpcdocs/pages/76513450/Basic+Job+Submission)  
[details: advanced submission](https://uiowa.atlassian.net/wiki/spaces/hpcdocs/pages/76513452/Advanced+Job+Submission)


!!! note "qsub [job script]"

    submit a job with batch script

!!! note "qstat -u [HawkID]"

    check the state of the submitted job

    Status:

    - r:   running
    - qw:  waiting in the queue

!!! note "qdel [job ID number]"

    cancel the submitted job either waiting in the queue or running

!!! note "qlogin [option]"

    interactive SGE session for a requested time period

    Options - SGE derivatives: 
    
    - -q [queue name]
    - -pe smp [number of slots]    
    - ...


## Sample batch script for a job submission

```bash

   #!/bin/bash

   #####Set Scheduler Configuration Directives#####
   # Set the name of the job.
   # This will be the first part of the job's .o (output) and .e (error) file names.
   #$ -N sleeper

   # By default, the job's working directory is the $HOME directory.
   # Here, set it the same as the current working directory when the job was submitted.
   # The job's .o (output) and .e (error) files will be written here.
   #$ -cwd

   # Send e-mail at beginning/end/suspension of job:
   #$ -m bes

   # E-mail address to send to:
   #$ -M [your Iowa email address]
   #####End Set Scheduler Configuration Directives#####

   #####Resource Selection Directives#####
   # Provide a comma-separated list of queues the scheduler can consider for this job:
   #$ -q [queue name]

   # Specify the number of slots the job will use:
   #$ -pe smp [number of slots]
   #####End Resource Selection Directives#####

   #####Load Modules####
   #module reset
   #module load ...
   #####Load Modules####

   #####Begin Compute Work#####
   # During the job, print information to stdout, which will be written into the job's output file:
   /bin/echo "Running on compute node: $(hostname)."
   /bin/echo "In directory: $(pwd)"
   /bin/echo "Starting on: $(date)"

   # Invoke the programs we want to run, and provide any necessary input parameters.
   # First, we start the "sleep" command so that it waits 60 seconds, then exits:
   sleep 60

   # Print the end date of the job before exiting:
   echo "Job ended: $(date)"
   #####End Compute Work#####
```
