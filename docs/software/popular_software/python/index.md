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



---


## Using Conda on HPC Systems

**Conda** is a popular tool for installing Python software along with its dependencies and managing virtual environments, especially on personal laptops or workstations.

You can install Conda via:

- **Miniconda**: A minimal installer that sets up the base Conda system, allowing you to install only the packages you need.
- **Anaconda**: A larger installer that includes the base Conda system plus a wide selection of commonly used scientific packages.

For more details, refer to the [Conda User Guide](https://docs.conda.io/projects/conda/en/latest/user-guide/index.html)

Conda provides functionality similar to what’s already available in the HPC environment, such as:

- Python installations
- Package management via `pip`
- Virtual environment support via `virtualenv`

While it’s possible to install Conda in your **home directory** or a **shared group drive**, it operates independently of the HPC module system. If you need specific Python packages not currently available in the HPC environment, consider requesting them from HPC staff before installing Conda yourself.

!!! danger "Important"
    A default Anaconda installation includes software that can interfere with graphical logins (e.g., FastX) by overriding system paths. See [this workaround](https://uiowa.atlassian.net/wiki/spaces/hpcdocs/pages/76513422/FastX+connections).


### Installing Anaconda on Argon

1. Download the installer from the Anaconda archive

    ```bash
    $ curl -RLO https://repo.anaconda.com/archive/Anaconda3-2024.10-1-Linux-x86_64.sh
    ```

2. Execute the installer

    ```bash
    $ bash Anaconda3-2024.10-1-Linux-x86_64.sh
    ```

    During installation, you’ll be asked whether to modify your shell configuration (e.g., .bashrc) to initialize Conda automatically at login. This may slightly slow down login times.

    If you choose to initialize Conda, the following block will be added to your `.bashrc`:

    ```bash
    # >>> conda initialize >>>
    # !! Contents within this block are managed by 'conda init' !!
    __conda_setup="$('$HOME/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
    if [ $? -eq 0 ]; then
        eval "$__conda_setup"
    else
        if [ -f "$HOME/anaconda3/etc/profile.d/conda.sh" ]; then
            . "$HOME/anaconda3/etc/profile.d/conda.sh"
        else
            export PATH="$HOME/anaconda3/bin:$PATH"
        fi
    fi
    unset __conda_setup
    # <<< conda initialize <<<
    ```

    You can comment out these lines later if you prefer not to auto-initialize Conda at login.

    ??? tip "If you skipped shell modification during installation but want to set the automatic Conda initialization afterward:"

        ```bash
        $ eval "$($HOME/anaconda3/bin/conda shell.bash hook)"
        $ conda init
        ```

        This will add the configuration lines above to your .bashrc. 


    Once the Conda is initiated, your prompt will show the base environment:

    ```bash
    (base) $
    ```

3. Create a New Environment

    ```bash
    (base) $ conda create -n someProject
    ```

    !!! tip
        Unlike the Python virtual environment, you can install different Python versions within the Conda virtual environment. You can still create a Conda environment with the specific Python version as well.

        ```bash
        (base) $ conda create -n someProject python=<Python_version>
        ```

4. Activate the Environment

    ```bash
    (base) $ source activate someProject
    ```
    Your prompt will change to:

    ```bash
    (someProject) $
    ```

5. Install Packages

    You can now search for and install packages. For example,

    ```bash
    (someProject) $ conda install numpy scipy matplotlib
    ```
    For more commands, see the [Conda Cheatsheet](https://docs.conda.io/projects/conda/en/stable/user-guide/cheatsheet.html).

6. Deactivate the Environment

    Once your work is done, you can get out of the Conda environment by

    ```bash
    (someProject) $ source deactivate
    ```
    This will return your shell to its previous state.


!!! tip "Additional Tip"

    - List the packages already installed in one of your Conda environments like so:
        ```bash
        $ conda list -n someProject
        ```
    - Remove a particular packag
        ```bash
        $ conda remove -n someProject opencv
        ```

    - Remove an entire Conda environment like so:
        ```bash
        $ conda remove -n someProject --all
        ```

    - List all remaining environments like so:
        ```bash
        $ conda info --envs
        ```

