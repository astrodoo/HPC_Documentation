# Getting Started with HPC 

<link rel="stylesheet" href="../../assets/stylesheets/buttons.css">

## What is an HPC?

At its core, a High Performance Computing (HPC) cluster is a group of uniformly configured compute nodes that work together—typically connected via high-bandwidth, low-latency networks—to solve large-scale computational problems. These problems often require more memory or processing power than a typical workstation or single server can provide.

When clustered, these nodes function as a unified system, enabling researchers to tackle complex tasks much more efficiently.

An HPC cluster typically includes:

- Compute nodes: Ranging from a few to thousands, these perform the actual computations.
- Login or staging nodes: Used for accessing the system and preparing jobs.
- Head nodes: Manage job scheduling, resource allocation, and data coordination.

---

## What is a Scheduler?

A scheduler is a software tool that manages and fairly distributes cluster resources among users. It works in tandem with a queuing system, which organizes jobs based on available resources or user access.

Schedulers allow users to select:

- Parallel environments (PEs): For jobs requiring inter-node communication.
- Special resources: Such as GPUs, co-processors, or extra memory.

Schedulers monitor job submissions and determine which jobs can run based on current resource availability. They may also prioritize jobs from users who use the system less frequently, ensuring equitable access and preventing resource monopolization.

---

## Roadmap for utilizing HPC cluster from scratch

1. Learn Basic Linux
    Our cluster runs CentOS Linux. To use it effectively, you'll need basic command-line skills—like navigating directories and editing files.

    - Recommended resource: The Linux Command Line ([free PDF](https://linuxcommand.org/tlcl.php))
    - Quick reference: [Linux Cheat Sheet](https://uiowa.atlassian.net/wiki/download/attachments/76513414/the-linux-command-line.pdf?version=1&modificationDate=1412807008197&cacheVersion=1&api=v2)

2. Map Your Work to the Cluster

    If your project:

    - Requires more memory than a desktop,
    - Needs fast turnaround,
    - Benefits from scheduled execution,

    ...then HPC may be a good fit.

    Ask yourself:

    - Does your code run on Linux?
    - Can it be executed in batch mode?
    - Is it a parallel (HPC) or serial (HTC) job?

3. Consider Compilation Needs

    If you're migrating code from another system, you may need to recompile it—especially if it uses MPI.
    See our notes on [compiling software](https://uiowa.atlassian.net/wiki/spaces/hpcdocs/pages/76513446/Compiling+Software)

4. Check Software Availability

    Browse our [Installed Software List](https://uiowa.atlassian.net/wiki/spaces/hpcdocs/pages/76513438/Software+Installations). If your required package isn’t listed, contact us. We may install it centrally or assist with installing it in your home directory.

5. Estimate Resource Requirements

    Knowing how much memory or how many processes your job needs helps ensure successful execution. Try running a small version of your job first, then scale up. You can also use our **development queue** for testing.






<!--
<html>
<a href="/get_started/..next..page"><button class="right-button" style="float: right;"></button></a>
</html>

-->
<br>
