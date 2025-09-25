
# Running R Programs in Job Scripts on Argon

To run an `R` program inside a job script on Argon, you must be able to execute the `R` script from the command line—without using the interactive `R` prompt. `R` provides the `Rscript` command for this purpose, which is available in all R modules on Argon.

## Basic Usage

If you normally process a dataset on your Windows or Unix workstation like this:

```bash
$ cd path/to/dataSet123
$ Rscript my/scripts/program.R inputDataSet123.txt > output123.txt
```

You can do the same on Argon by composing a job script that loads the appropriate R modules:

```bash
module reset
module load r
cd path/to/dataSet123
Rscript my/scripts/program.R inputDataSet123.txt > output123.txt
```

!!! tip "Using SGE and Scratch Filesystems for Better Performance"
    To improve performance by following [HTC Best Practice](https://uiowa.atlassian.net/wiki/spaces/hpcdocs/pages/76513456/Best+Practices+for+High+Throughput+Jobs), you can use SGE to temporarily store output on Argon's /localscratch filesystem:

    ```bash
    #$ -j y
    #$ -o /localscratch
    
    module reset
    module load r
    cd path/to/dataSet123
    Rscript my/scripts/program.R inputDataSet123.txt
    mv $SGE_STDOUT_PATH .
    ```

!!! danger "Avoiding R CMD BATCH"

    Some tutorials suggest using the older `R CMD BATCH program.R` convention. However, this approach has several drawbacks, especially on HPC systems:

    - It simulates an interactive session and prints output inline with the script, making it harder to read or parse.
    - It does not print to standard output (stdout), so you can't use SGE or redirection (>).
    - It always creates a file named `program.Rout` in the current directory, which may not align with your input/output locations and can cause performance issues.
    

    <mark>**Recommendation: Use `Rscript` instead of `R CMD BATCH`**</mark>


---

## Running MPI Jobs with R (Using R-snow)

Running MPI jobs with R with the `R-snow` package requires special handling.

### Single-Node Execution

If all MPI processes run on a single host, you can start R normally and spawn MPI ranks within the script.

### Multi-Node Execution

For multi-node jobs, processes must be spawned using `mpirun`. This also works for single-node jobs. Since `mpirun` starts `R`, you need a wrapper to distinguish between primary and secondary processes. This wrapper is called `RMPISNOW`.

#### Launching the Job

```bash
mpirun -np <num_processes> RMPISNOW CMD BATCH --slave sample_script.R
```

- The `SGE` slot request must be **one greater** than the number of workers.
- If no additional slots are requested for memory, `mpirun` will use the `SGE` environment settings.

You can also simplify the command:
```bash
mpirun RMPISNOW CMD BATCH --slave sample_script.R
```

#### Inside the R Script

To reference the snow cluster created by mpirun, use:

```bash
mpi.universe.size() - 1     # Number of workers

cl <- getMPIcluster()       # Create cluster object
stopCluster(cl)             # Stop the cluster
mpi.quit()                  # Exit the R session
```
> `mpi.universe.size()` is the total number of MPI processes, so the number of workers is set to be one less.


!!! warning 

    Note: Rscript cannot be used with the `RMPISNOW` wrapper, as it directly calls R. Alternatively, you can run the command as:
    
    ```bash
    mpirun RMPISNOW --slave < sample_script.R
    ```
