# md5-compare-Wdask
This repository contains a Python script for comparing files between two directories using their MD5 checksums, leveraging the distributed computing capabilities of Dask to efficiently handle large datasets across multiple cores and machines.

Overview
The script computes MD5 checksums for all non-hidden files in two specified directories (a master directory and an input directory), compares them, and identifies files present in the input directory but not in the master directory based on their checksums. This process is parallelized using Dask, making it highly efficient for large sets of files or directories with substantial amounts of data.

Prerequisites
Python 3.6 or later
Dask Distributed
Access to a multi-core machine or a cluster of machines for distributed processing
Setup
1. Install Python
Ensure that Python 3.6 or newer is installed on your system. You can download Python from the official website.


2. Installing Dask
  You first need to ensure Dask is installed on the scheduler and worker machines:
  `pip3 install "dask[complete]"` 


4. Configure Dask Cluster
Local Cluster
For local testing or development, you can use Dask's ability to create a cluster on your machine utilizing its cores. This is automatically handled when you instantiate a Client object without specifying a scheduler address in the script.

Distributed Cluster
For production or processing large datasets, set up a Dask distributed cluster:

- Scheduler: Start a Dask scheduler on one of the machines:
  `python3 -m distributed.cli.dask_scheduler`

- Workers: Start Dask workers on each machine that should participate in the cluster, using the scheduler's address:
  `python3 -m distributed.cli.dask_worker tcp://schedulerAddress:8786 --nthreads 16 --memory-limit 32GB`
  Adjust --nthreads and --memory-limit according to your machine's capabilities.

  
4. Clone the Repository
Clone this repository to get the script


Usage
1. Edit the Script: Open the script in your preferred text editor and modify the dask_scheduler_address variable to point to your Dask scheduler's address (if using a distributed cluster).

2. Run the Script: Execute the script and follow the on-screen prompts to enter the paths of the master and input directories:
   `python3 main.py`
3. Review the Output: Upon completion, the script outputs a list of files present in the input directory but not in the master directory, based on MD5 checksum comparison. This list is saved to a file named FILES_NOT_IN_MASTER.txt in the input directory.


Monitoring
Access the Dask dashboard at http://scheduler-address:8787 to monitor task progress, worker status, and more. This provides valuable insights into the execution and helps in identifying bottlenecks or issues.
