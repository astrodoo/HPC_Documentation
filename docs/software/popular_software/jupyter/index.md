# Running a Jupyter Notebook on Argon

Although Argon is not designed to host a full JupyterHub installation, you can still run a **Jupyter Notebook** on Argon and connect to it using a web browser on your local machine. This requires setting up a network path, typically using **SSH tunneling**, between the system running the notebook (Argon) and your local computer.

To use a browser on your local machine, one end of the SSH tunnel must be on your computer.

The instructions below are specific to the Argon HPC system, including how to select a Python environment and run Jupyter.

!!! danger "Always run Jupyter Notebook on **compute nodes** using the SGE scheduler. Running it on login nodes can negatively impact system performance for others."

1. Create a Script to Launch Jupyter Notebook

    ```bash
    $ mkdir -p $HOME/bin
    $ echo -e '#!/bin/bash\njupyter notebook --ip=$(hostname -f) --no-browser --port=8080' > $HOME/bin/notebook.sh
    ```

    - This creates a directory for your personal scripts and adds a script to launch Jupyter Notebook.
    - The port number `8080` can be replaced with any available four-digit port.

    ```bash title="Contents of notebook.sh"
    #!/bin/bash
    jupyter notebook --ip=$(hostname -f) --no-browser --port=8080
    ```

2. Convert the script to be executable

    ```bash
    $ chmod +x $HOME/bin/notebook.sh
    ```

3. Load required modules 

    ```bash
    $ module load python
    $ module load py-jupyter
    ```
    !!! warning "important"
        The default Python version is 2.7, so you should load the Python module to use a later version of Python. Check the available Python versions by:
        ```bash
        $ module spider python
        ```
    
        You will need to load the required Python packages to use in the notebook. For example, 
        ```bash
        $ module load py-numpy
        $ module load py-matplotlib
        ```
    
        For more information, refer to the [Module page](../../modules#examples).

        Alternatively, you can activate a Python virtual environment or Conda virtual environment to build the list of packages you need. See [Python page](../python) for the detailed information. 


4. Launch Jupyter Notebook on a Compute Node

    Use the SGE scheduler to request compute resources:
    ```bash
    $ qrsh -q UI -N Jupyter -pe smp 2 -cwd $HOME/bin/notebook.sh
    ```

    In this example, it requests `UI` queue with 2 slots (`-pe smp 2`) and the name of the job is Jupyter. The `-cwd` flag indicates that the Jupyter Notebook will access the current directory. You can modify the queue, number of slots, and the Job name.

    If successful, you’ll see output like:

    
