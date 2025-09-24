# Software Modules

High-Performance Computing (HPC) environments support a wide range of software applications, libraries, and compilers. Efficiently managing these resources can be challenging due to differing versions, configurations, and dependencies, which may lead to conflicts if not properly handled. 

To mitigate this, HPC systems utilize a **module system**. Software packages are installed in non-standard locations to avoid clashes with system-wide paths. Instead of altering global settings, users dynamically configure their environments using modules. With simple commands, they can load, unload, and switch between different software versions, ensuring a clean, consistent, and personalized computing environment.

!!! Tip "Software Stack"
    Software packages in HPC environments are organized into sets known as **`stacks`**. <mark>Each stack contains a collection of software built with a consistent set of dependencies, ensuring compatibility within the stack.</mark> This approach allows multiple versions of the same software to coexist, each within its own well-defined environment. While switching between versions of a specific package can be more complex under this scheme, the recommended solution is to load the appropriate stack in a separate SSH session. This ensures a clean and conflict-free environment tailored to the specific version requirements.

    ```bash 
    dooyoon@argon-login-5 ~> module spider stack
    
    -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      stack:
    -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
         Versions:
            stack/legacy
            stack/2019.1
            stack/2020.1
            stack/2020.2-base_arch
            stack/2020.2
            stack/2021.1-base_arch
            stack/2021.1
            stack/2022.1-base_arch
            stack/2022.1
            stack/2022.2-base_arch
            stack/2022.2
    ```

## Module Commands

| Command | Description|
| ------- | ---------- |
| <pre><code>module list</code></pre> | Display the software you have loaded in your environment. |
| <pre><code>module avail</code></pre> | Display all installed modules under current stack matching the `<module_name>`.|
| <pre><code>module spider &#60;module_name&#62; </code></pre> | Display all installed modules available matching the `<module_name>`.|
| <pre><code>module show &#60;module_name&#62; </code></pre>  | Displays system variables that are set/modified when loading module `<module_name>`. This can be helpful for locating the executables that are provided by the module.|
|<pre><code>module load &#60;module_name&#62;</code></pre>|Load a software module in your environment|
|<pre><code>module unload &#60;module_name&#62;</code></pre>|Unload a specific software package from your environment|
|<pre><code>module reset</code></pre>| Configure back to default set |
|<pre><code>module purge</code></pre>| Unload all software modules from your environment|
|<pre><code>module save &#60;module_list_name&#62; </code></pre>| Save the list of current modules to the name `module_list_name`|
|<pre><code>module restore &#60;module_list_name&#62;</code></pre>| Restore the list of modules from `module_list_name`|
|<pre><code>module help</code></pre>| Display a help menu for the module command|

## Examples

```bash title="List current modules"

dooyoon@argon-login-5 ~> module list

Currently Loaded Modules:
  1) stack/2021.1              4) expat/2.2.10_gcc-9.3.0    7) libxml2/2.9.10_gcc-9.3.0  10) libffi/3.3_gcc-9.3.0      13) readline/8.1_gcc-9.3.0            16) xz/5.2.5_gcc-9.3.0
  2) bzip2/1.0.8_gcc-9.3.0     5) gdbm/1.19_gcc-9.3.0       8) tar/1.34_gcc-9.3.0        11) ncurses/6.2_gcc-9.3.0     14) sqlite/3.35.3_gcc-9.3.0           17) zlib/1.2.11_gcc-9.3.0
  3) libbsd/0.10.0_gcc-9.3.0   6) libiconv/1.16_gcc-9.3.0   9) gettext/0.21_gcc-9.3.0    12) openssl/1.1.1k_gcc-9.3.0  15) util-linux-uuid/2.36.2_gcc-9.3.0  18) python/3.8.8_gcc-9.3.0

```

```bash title="Find the desired Python version"

dooyoon@argon-login-5 ~> module spider python

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  python:
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
     Versions:
        python/2.7.13_parallel_studio-2017.1
        python/2.7.13
        ...
        python/3.10.8_gcc-9.5.0-dev
        python/3.10.8_gcc-9.5.0
        python/3.10.8_intel-2021.7.1-dev
        python/3.10.8_intel-2021.7.1
        ...



dooyoon@argon-login-5 ~> module spider python/3.10.8_gcc-9.5.0

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  python: python/3.10.8_gcc-9.5.0
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    You will need to load all module(s) on any one of the lines below before the "python/3.10.8_gcc-9.5.0" module is available to load.

      stack/2022.2
      stack/2022.2-base_arch
 
    Help:
      The Python programming language.

```

!!! tip
    To load ```Python 3.10.8```, you need to load ```stack/2022.2```. 

```bash title="Load the Python version"

dooyoon@argon-login-5 ~> module load stack/2022.2

The following have been reloaded with a version change:
  1) stack/2021.1 => stack/2022.2


dooyoon@argon-login-5 ~> module load python/3.10.8_gcc-9.5.0


dooyoon@argon-login-5 ~> module list

Currently Loaded Modules:
  1) stack/2022.2              5) expat/2.4.8_gcc-9.5.0      9) libiconv/1.16_gcc-9.5.0   13) pigz/2.7_gcc-9.5.0        17) libffi/3.4.2_gcc-9.5.0      21) util-linux-uuid/2.38.1_gcc-9.5.0
  2) bzip2/1.0.8_gcc-9.5.0     6) ncurses/6.3_gcc-9.5.0     10) xz/5.2.7_gcc-9.5.0        14) zstd/1.5.2_gcc-9.5.0      18) libxcrypt/4.4.31_gcc-9.5.0  22) python/3.10.8_gcc-9.5.0
  3) libmd/1.0.4_gcc-9.5.0     7) readline/8.1.2_gcc-9.5.0  11) zlib/1.2.13_gcc-9.5.0     15) tar/1.34_gcc-9.5.0        19) openssl/1.1.1s_gcc-9.5.0
  4) libbsd/0.11.5_gcc-9.5.0   8) gdbm/1.23_gcc-9.5.0       12) libxml2/2.10.3_gcc-9.5.0  16) gettext/0.21.1_gcc-9.5.0  20) sqlite/3.39.4_gcc-9.5.0
```

!!! note "Python and R packages"
    
    Python and R packages have a name convention starting with "py-" and "r-", respectively. For example, the module for the `numpy` package is named as `py-numpy`:


    ```bash
    dooyoon@argon-login-5 ~> module avail py-numpy

    ------------------------------------------------------------------------------------- /opt/ssoft/modules/2021.1/packages --------------------------------------------------------------------------------------
    py-numpy/1.19.5_gcc-9.3.0    py-numpydoc/1.1.0_gcc-9.3.0
    ```

    To check all available packages, you will need to add patterns and Regular Expression (regex) option (`-r`) to the module search command:

    ```bash
    dooyoon@argon-login-5 ~> module -r avail ^py
    
    ------------------------------------------------------------------------------------- /opt/ssoft/modules/2021.1/packages --------------------------------------------------------------------------------------
       py-absl-py/0.10.0_gcc-9.3.0                     py-hypothesis/5.3.0_gcc-9.3.0                 py-pexpect/4.7.0_gcc-9.3.0                          py-simplejson/3.16.0_gcc-9.3.0
       py-agate-dbf/0.2.1_gcc-9.3.0                    py-idna/2.8_gcc-9.3.0                         py-pickleshare/0.7.5_gcc-9.3.0                      py-sip/4.19.21_gcc-9.3.0-qt5
       py-agate-excel/0.2.3_gcc-9.3.0                  py-imageio-ffmpeg/0.4.3_gcc-9.3.0             py-pillow/7.2.0_gcc-9.3.0                           py-sip/4.19.21_gcc-9.3.0                         (D)
       py-agate-sql/0.5.4_gcc-9.3.0                    py-imageio/2.9.0_gcc-9.3.0                    py-pip/20.2_gcc-9.3.0                               py-six/1.15.0_gcc-9.3.0
    ...
    ```

---

## Using Environment Modules with SGE Jobs and `qlogin`

### `qlogin` Sessions

For interactive sessions launched with `qlogin`, a **fresh environment** is created. This means that any environment modules loaded prior to launching `qlogin` will **not** be available in the session.

For more details, refer to the [Qlogin for Interactive Sessions](https://uiowa.atlassian.net/wiki/spaces/hpcdocs/pages/76513454/Qlogin+for+Interactive+Sessions).


### Standard `qsub` Jobs

For standard batch jobs submitted via `qsub`, the **entire environment** from the submit host is passed to the job **by default**, due to the `-V` flag being set in the default SGE request. This includes:

- The environment set up by loaded modules.
- The list of loaded modules themselves.

<mark> However, it is **recommended** to explicitly include `module load` statements in your job script rather than relying on the inherited environment.</mark> This ensures:

- Greater reproducibility.
- Clear documentation of dependencies.

To avoid conflicts or unintended behavior, add the lines below to your job script:

```bash
module purge
module load stack/<desired stack>
module load <package>
```

### High Throughput / High Volume Computing (HTC/HVC) Jobs

<mark> For HTC or HVC workloads involving **thousands of jobs**, it is **not advisable** to load modules within each job script.</mark> Doing so can:

- Overload the module system.
- Lead to job failures due to rapid, repeated module loads.

Therefore, it is recommended to 

- Load all necessary modules **before** job submission.
- Ensure the submission environment is correctly configured.
- Avoid loading modules or module sets in your `~/.bashrc` file.
- Disable any default module sets if configured.
- You may include comments in your job scripts to document which modules are expected, but **do not** perform actual module loads within the script.

