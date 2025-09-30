# Establishing Python Environment


## Available Python Environments on HPC Systems

The HPC systems provide a variety of Python installations for users to choose from. To view the available Python modules, run:


```bash
dooyoon@argon-login-6 ~> module spider python

----------------------------------------------------------------------------
  python:
----------------------------------------------------------------------------
     Versions:
        python/2.7.13_parallel_studio-2017.1
        python/2.7.13
        ...
        python/3.10.8_gcc-9.5.0-dev
        python/3.10.8_gcc-9.5.0
        python/3.10.8_intel-2021.7.1-dev
        python/3.10.8_intel-2021.7.1

```
Python packages in the module environment have a naming convention with the prepix ```py-xxx```. For more details, Refer to the [Software Modules](../../modules).

---

## Python Virtual Environment


**Python virtual environments** is a self-contained Python setup with its own:

- Python interpreter
- `pip` installer
- Package directory


This allows you to modify or test environments independently, isolate codebases with conflicting dependencies, and manage multiple projects more effectively.

!!! warning 
    The Python version will be fixed to the one that is used to create the virtual environment. Therefore, you should carefully choose the Python version in the stack environment and load it before establishing the environment. 

Follow steps below to create a virtual environment and install packages:

1. Check Available Python Modules
    ```bash
    $ module spider python
    
    ----------------------------------------------------------------------------
      python:
    ----------------------------------------------------------------------------
         Versions:
            python/2.7.13_parallel_studio-2017.1
            python/2.7.13
            ...
            python/3.10.8_gcc-9.5.0-dev
            python/3.10.8_gcc-9.5.0
            python/3.10.8_intel-2021.7.1-dev
            python/3.10.8_intel-2021.7.1
    
    ```

2. Load the Desired Python Module
    ```bash
    $ module spider python/3.10.8_gcc-9.5.0
    
    -----------------------------------------------------------------------------------------------------------------------------------------
      python: python/3.10.8_gcc-9.5.0
    -----------------------------------------------------------------------------------------------------------------------------------------
        You will need to load all module(s) on any one of the lines below before the "python/3.10.8_gcc-9.5.0" module is available to load.
          stack/2022.2
          stack/2022.2-base_arch
          ...
    $ module load stack/2022.2
    $ module load python/3.10.8_gcc-9.5.0
    ```

3. Create a Directory for Virtual Environments if you don't have it yet
    ```bash
    $ mkdir $HOME/virtenvs
    ```

    !!! tip
        You'll probably make a few environments for testing and unrelated tasks, and it's common convention to create a directory to keep them organized:


4. Create a Virtual Environment
    ```bash
    $ python -m venv $HOME/virtenvs/someProject
    ```
    This creates a directory named someProject containing the environment configuration.

    If you want the environment to include packages from the loaded module (e.g., MKL-linked NumPy/SciPy), use:
    ```bash
    $ python -m venv --system-site-packages $HOME/virtenvs/someProject
    ```

5. Activate the virtual environment
    ```bash
    $ source $HOME/virtenvs/someProject/bin/activate
    ```
    Your shell prompt will change to indicate the active environment:
    ```
    (someProject) $
    ```

6. Upgrade Core Tools

    Before installing packages, upgrade pip, setuptools, and wheel:

    ```bash
    (someProject) $ pip install -U pip setuptools wheel
    ```

7. Install Packages

    ```bash
    (someProject) $ pip install -U package1 package2 package3
    ```

    !!! tip
        The `-U` option upgrades all specified packages to the newest available version. Omit this option if you don't want to upgrade packages. For more options with `pip install`, see the [pip documentation](https://pip.pypa.io/en/stable/cli/pip_install/).

8. Deactivate the Environment

    When you're done, you can get out of the virtual environment by the following command:
    ```bash
    (someProject) $ deactivate
    ```
    This restores your shell to its previous state and removes the (someProject) prompt.

9. Reuse the Environment

    To reuse the environment later (e.g., in a job script or interactive session), simply activate it again:

    ```bash
    $ source $HOME/virtenvs/someProject/bin/activate
    ```

    You can continue installing, removing, or running packages as needed.

    !!! tip 
        To use the virtual environment in a cluster job script, simply activate it there the same way.

