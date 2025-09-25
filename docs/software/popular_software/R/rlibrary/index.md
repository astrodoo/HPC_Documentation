# Adding R programs to a personal library

There are two main approaches to managing R packages in a personal library:

1. **Global Personal R Library**  
   Create a personal library in your home directory for a specific version of R. This allows packages to be available whenever you use that version.

2. **Project-Specific Environments with Packrat**  
   Use [Packrat](https://rstudio.github.io/packrat/) to create isolated, portable environments for each R project. This ensures reproducibility and avoids package conflicts across projects.

---

## Option 1: Global Personal R Library

Installing R packages locally is straightforward:

1. Load the R module
    
    ```bash
    dooyoon@argon-itf-login-3 ~> module load r

    dooyoon@argon-itf-login-3 ~> module list

    Currently Loaded Modules:
      1) stack/2021.1                      14) gdbm/1.19_gcc-9.3.0             27) xcb-proto/1.14.1_gcc-9.3.0     40) graphite2/1.3.13_gcc-9.3.0      53) openjdk/11.0.8_10_gcc-9.3.0
      2) bzip2/1.0.8_gcc-9.3.0             15) perl/5.32.1_gcc-9.3.0           28) xextproto/7.3.0_gcc-9.3.0      41) harfbuzz/2.6.8_gcc-9.3.0        54) gobject-introspection/1.56.1_gcc-9.3.0
      3) font-util/1.3.2_gcc-9.3.0         16) libbsd/0.10.0_gcc-9.3.0         29) xproto/7.0.31_gcc-9.3.0        42) icu4c/67.1_gcc-9.3.0            55) libxft/2.3.2_gcc-9.3.0
      4) libiconv/1.16_gcc-9.3.0           17) expat/2.2.10_gcc-9.3.0          30) xtrans/1.3.5_gcc-9.3.0         43) intel-mkl/2020.4.304_gcc-9.3.0  56) pango/1.41.0_gcc-9.3.0
      5) libxml2/2.9.10_gcc-9.3.0          18) openssl/1.1.1k_gcc-9.3.0        31) libxcb/1.14_gcc-9.3.0          44) libjpeg-turbo/2.0.6_gcc-9.3.0   57) pcre2/10.35_gcc-9.3.0
      6) util-linux-uuid/2.36.2_gcc-9.3.0  19) sqlite/3.35.3_gcc-9.3.0         32) libxext/1.3.3_gcc-9.3.0        45) libpng/1.6.37_gcc-9.3.0         58) readline/8.1_gcc-9.3.0
      7) fontconfig/2.13.1_gcc-9.3.0       20) python/3.8.8_gcc-9.3.0          33) renderproto/0.11.1_gcc-9.3.0   46) libtiff/4.1.0_gcc-9.3.0         59) scrnsaverproto/1.2.2_gcc-9.3.0
      8) freetype/2.10.4_gcc-9.3.0         21) glib/2.66.8_gcc-9.3.0           34) libxrender/0.9.10_gcc-9.3.0    47) libx11/1.7.0_gcc-9.3.0          60) libxscrnsaver/1.2.2_gcc-9.3.0
      9) tar/1.34_gcc-9.3.0                22) inputproto/2.3.2_gcc-9.3.0      35) pixman/0.40.0_gcc-9.3.0        48) libice/1.0.9_gcc-9.3.0          61) tcl/8.6.11_gcc-9.3.0
     10) gettext/0.21_gcc-9.3.0            23) kbproto/1.0.7_gcc-9.3.0         36) cairo/1.16.0_gcc-9.3.0         49) libsm/1.2.3_gcc-9.3.0           62) tk/8.6.10_gcc-9.3.0
     11) libffi/3.3_gcc-9.3.0              24) libpthread-stubs/0.4_gcc-9.3.0  37) libunistring/0.9.10_gcc-9.3.0  50) libxmu/1.1.2_gcc-9.3.0          63) xz/5.2.5_gcc-9.3.0
     12) pcre/8.44_gcc-9.3.0               25) libxau/1.0.8_gcc-9.3.0          38) libidn2/2.3.0_gcc-9.3.0        51) libxt/1.1.5_gcc-9.3.0           64) zlib/1.2.11_gcc-9.3.0
     13) berkeley-db/18.1.40_gcc-9.3.0     26) libxdmcp/1.1.2_gcc-9.3.0        39) curl/7.76.0_gcc-9.3.0          52) ncurses/6.2_gcc-9.3.0           65) r/4.0.5_gcc-9.3.0
    ```

2. Launch `R`

    ```bash
    dooyoon@argon-itf-login-3 ~> R

    R version 4.0.5 (2021-03-31) -- "Shake and Throw"
    Copyright (C) 2021 The R Foundation for Statistical Computing
    Platform: x86_64-pc-linux-gnu (64-bit)
    
    R is free software and comes with ABSOLUTELY NO WARRANTY.
    You are welcome to redistribute it under certain conditions.
    Type 'license()' or 'licence()' for distribution details.
    
      Natural language support but running in an English locale
    
    R is a collaborative project with many contributors.
    Type 'contributors()' for more information and
    'citation()' on how to cite R or R packages in publications.
    
    Type 'demo()' for some demos, 'help()' for on-line help, or
    'help.start()' for an HTML browser interface to help.
    Type 'q()' to quit R.
    
    [Previously saved workspace restored]
    
    > 
    ```


3. Install a package

    Replace "package_name" with the desired package name: 

    ```bash
    > install.packages("package_name", repos = "http://cran.r-project.org")
    ```

!!! warning "Not Writable warning"

    You may see a warning like:

    ```bash
    Warning in install.packages("package_name", repos = "http://cran.r-project.org") : 'lib = "/opt/R/3.0.2/lib64/R/library"' 
    is not writable Would you like to use a personal library instead? (y/n)
    ```

    Select y to use a personal library.
    Select y again when prompted to create the directory.

    The package will then be installed into your newly created personal library.


## Option 2: Packrat Project Directory

Packrat is an R package that enables isolated environments for each project. On the Argon HPC cluster:

- Packrat is available starting with R version 3.3.2.
- For newer versions (e.g., modules named r-#.#.# from 3.6.2 onward or stack modules like YYYY.# from 2019.1), the r-packrat module must be loaded manually.

1. Create a project directory

    ```bash
    dooyoon@argon-itf-login-3 ~> mkdir ~/myproject
    dooyoon@argon-itf-login-3 ~> cd ~/myproject
    ```

2. Start `R` (follow the step 1 and 2 in the Option 1) and initialize Packrat

    ```
    packrat::init()
    ```
From this point on, any packages you install will be stored in the project-specific library.

### Resuming Packrat Project

- `cd` into the project directory.
- Start `R` — Packrat will load automatically.

### Using Packrat from the Shell

```bash
dooyoon@argon-itf-login-3 ~> mkdir ~/someproject
dooyoon@argon-itf-login-3 ~> cd ~/someproject
dooyoon@argon-itf-login-3 ~> Rscript -e 'packrat::init(enter=FALSE)'
dooyoon@argon-itf-login-3 ~> Rscript -e 'install.packages(c("brms", "rstanarm"))'
```




