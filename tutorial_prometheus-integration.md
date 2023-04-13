Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Integrate with Prometheus

Share Feedback

On this page

  * Prerequisites
  * Procedure
  * Example Configurations
  * Performance Metrics Available to Prometheus
  * MongoDB Metric Labels
  * MongoDB Information Metrics
  * Hardware Metrics
  * Hardware Metric Labels

Prometheus collects metrics from configured targets at given intervals,
evaluates rule expressions, displays the results, and can trigger alerts when
it observes specific conditions.

Our integration allows you to configure Atlas to send metric data about your
deployment to your Prometheus instance.

## Prerequisites

  * Prometheus integration is available only on `M10+` clusters.

  * Have a working Prometheus instance. To set up a working instance, see their Installation Guide.

  * Add the IP of the device hosting your Prometheus instance to the IP Access List.

## Note

If you add `0.0.0.0/0` to the IP Access List, which allows cluster access from
anywhere in the public internet, Atlas disables the Prometheus integration.

If `0.0.0.0/0` is already on the IP Access List, Atlas stops you from
configuring the Prometheus integration.

  * (Optional) Use Grafana to visualize your Prometheus metrics.

## Procedure

To configure an Atlas integration with Prometheus:

1

### Navigate to your Project Integrations.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Next to the Projects menu, expand the Options menu, then click Integrations.

2

### Click Configure for the Prometheus integration card.

3

### Enter your preferred username and password.

## Important

Copy your username and password in a secure location. You can't access the
password after you leave this screen.

4

### Select your preferred service discovery method.

Discovery Method

|

Description  
  
|  
  
HTTP SD

|

This method requires Prometheus v2.28 and later. It automatically generates
the scrape_config part of your configuration file to discover targets over an
HTTP endpoint.  
  
File Service Discovery

|

This method allows Prometheus to read YAML or JSON documents to configure the
targets to scrape from. You are responsible for providing the targets by
making a request to the Discovery API and storing its results in a
`targets.json` file.

To make the request, substitute the placeholder text in one of the following
tabs or create your own script in another language.

Shell Command

Python Script

    
    
    | curl --header 'Accept: application/json'  
      
    # Sets the `Authorization` header on every scrape request with the  
    # username and password from the previous step.  
    --user <username>:<password>  
    # The URL that Prometheus fetches the targets from.  
    # Replace the <group-id> with the project ID of your Atlas instance.  
    --request GET "https://cloud.mongodb.com/prometheus/v1.0/groups/<group_id>/discovery"  
  
To learn more about the Discovery API, see Return the Latest Targets for
Prometheus.

5

### Click Save.

6

### View Your Cluster Metrics on Prometheus.

  1. Copy the generated snippet into the scrape_configs section of your configuration file and substitute the placeholder text.

For an example of the configuration file in either method, see Example
Configurations.

  2. Restart your Prometheus instance.

  3. In your Prometheus instance, click `Status` in the top navigation bar, and click `Targets` to see the metrics of your deployment.

## Example Configurations

The following shows examples of the configuration file when you use the HTTP
SD or File Service Discovery method.

The configuration file in both methods contains the following fields:

Field

|

Description  
  
|  
  
`scrape_interval`

|

Time that indicates how frequently to scrape targets. This setting supports a
minimum time of 10s.  
  
`job_name`

|

Human-readable label assigned to scraped metrics.  
  
`metrics_path`

|

HTTP resource path that indicates where to fetch metrics from targets.  
  
`scheme`

|

Protocol scheme that you want to configure for requests.  
  
`basic_auth`

|

Authorization header to use on every scrape request.  
  
### HTTP SD

The HTTP SD method also contains the `http_sd_configs` field with the
following sub-fields:

Field

|

Description  
  
|  
  
`url`

|

URL from which Prometheus fetches the targets.  
  
`refresh_interval`

|

Time that indicates when to re-query the endpoint.  
  
`basic_auth`

|

Credentials to use for authenticating to the API server.  
      
    
    global:  
      
      scrape_interval: 15s  
      
    scrape_configs:  
      
      - job_name: "Cloud-Testing-mongo-metrics"  
        scrape_interval: 10s  
        metrics_path: /metrics  
        scheme : https  
        basic_auth:  
          username: prom_user_618d48e05277a606ed2496fe  
          password: fSIMUngfTmOTVEB4  
        http_sd_configs:  
          - url: https://cloud.mongodb.com/prometheus/v1.0/groups/618d48e05277a606ed2496fe/discovery  
          refresh_interval: 60s  
          basic_auth:  
            username: prom_user_618d48e05277a606ed2496fe  
            password: fSIMUngfTmOTVEB4  
  
### File Service Discovery

The File Service Discovery method also contains the `file_sd_configs` field
with the following sub-field:

Field

|

Description  
  
|  
  
`files`

|

List that contains the files from which to extract the metrics scraping
targets.  
      
    
    global:  
      
      scrape_interval: 15s  
      
    scrape_configs:  
      
      - job_name: "Cloud-Testing-mongo-metrics"  
        scrape_interval: 10s  
        metrics_path: /metrics  
        scheme : https  
        basic_auth:  
          username: prom_user_618d48e05277a606ed2496fe  
          password: fSIMUngfTmOTVEB4  
        file_sd_configs:  
          - files:  
            - /usr/local/etc/targets.json  
  
## Performance Metrics Available to Prometheus

The following metrics are available when you use the Prometheus integration
with your Atlas cluster:

  * MongoDB Metric Labels

    * serverStatus metrics

    * replSetStatus metrics

  * MongoDB Information Metrics

  * Hardware Metrics

## MongoDB Metric Labels

Each MongoDB metric contains the following labels:

Label

|

Description  
  
|  
  
`group_id`

|

Unique hexadecimal digit string that identifies the project.  
  
`org_id`

|

Unique hexadecimal digit string that identifies the organization.  
  
`cl_role`

|

Human readable label that defines the cluster role.  
  
`cl_name`

|

Human-readable label that identifies the cluster.  
  
`rs_nm`

|

Human-readable label that identifies the replica set.  
  
`rs_state`

|

Number that indicates the replica set state.  
  
`process_port`

|

Port on which the process runs.  
  
## MongoDB Information Metrics

`mongodb_info` is a gauge that always has the value of `1`. This metric
contains all the MongoDB Metric Labels and also the following labels:

Label

|

Description  
  
|  
  
`mongodb_version`

|

String that represents the major, minor, and patch versions.  
  
`replica_state_name`

|

String that indicates the replica set member status.  
  
`process_type`

|

String that indicates the process running. Its values can be `mongod`,
`mongos`, or `config`.  
  
## Hardware Metrics

## Note

You can also view descriptions of each hardware metric in the Prometheus
expression browser.

Name

|

Type

|

Description  
  
||  
  
`hardware_disk_metrics_disk_space_free_bytes`

|

Gauge

|

Disk space available in the mounted file system.  
  
`hardware_disk_metrics_disk_space_used_bytes`

|

Gauge

|

Disk space used in the mounted file system.  
  
`hardware_disk_metrics_read_count`

|

Counter

|

Number of read I/O's processed.  
  
`hardware_disk_metrics_read_time_milliseconds`

|

Counter

|

Total wait time for read requests.  
  
`hardware_disk_metrics_sectors_read`

|

Counter

|

Number of sectors read.  
  
`hardware_disk_metrics_sectors_written`

|

Counter

|

Number of sectors written.  
  
`hardware_disk_metrics_total_time_milliseconds`

|

Counter

|

Total time this block device is active.  
  
`hardware_disk_metrics_weighted_time_io_milliseconds`

|

Counter

|

Weighted time spent doing I/O's.  
  
`hardware_disk_metrics_write_count`

|

Counter

|

Number of write I/O's processed.  
  
`hardware_disk_metrics_write_time_milliseconds`

|

Counter

|

Total wait time for write requests.  
  
`hardware_platform_num_logical_cpus`

|

Gauge

|

Number of logical CPUs usable by the current process.  
  
`hardware_process_cpu_children_kernel_milliseconds`

|

Counter

|

Amount of time scheduled in kernel mode for this process to wait for children.  
  
`hardware_process_cpu_children_user_milliseconds`

|

Counter

|

Amount of time scheduled in user mode for this process to wait for children.  
  
`hardware_process_cpu_kernel_milliseconds`

|

Counter

|

Amount of time scheduled in kernel mode for this process.  
  
`hardware_process_cpu_user_milliseconds`

|

Counter

|

Amount of time scheduled in user mode for this process.  
  
`hardware_system_cpu_guest_milliseconds`

|

Counter

|

Time spent running a virtual CPU for the guest operating systems under the
control of the Linux kernel.  
  
`hardware_system_cpu_guest_nice_milliseconds`

|

Counter

|

Time spent running a guest with an adjusted niceness.  
  
`hardware_system_cpu_idle_milliseconds`

|

Counter

|

Time spent in the idle task.  
  
`hardware_system_cpu_io_wait_milliseconds`

|

Counter

|

Time waiting for I/O to complete.  
  
`hardware_system_cpu_irq_milliseconds`

|

Counter

|

Time spent servicing interrupts.  
  
`hardware_system_cpu_kernel_milliseconds`

|

Counter

|

Time spent in system mode.  
  
`hardware_system_cpu_nice_milliseconds`

|

Counter

|

Time spent in user mode with low priority (nice).  
  
`hardware_system_cpu_soft_irq_milliseconds`

|

Counter

|

Time spent servicing `softirqs`.  
  
`hardware_system_cpu_steal_milliseconds`

|

Counter

|

Time spent in other operating systems when running in a virtual environment.  
  
`hardware_system_cpu_user_milliseconds`

|

Counter

|

Time spent in user mode.  
  
`hardware_system_memory_buffers_kilobytes`

|

Gauge

|

Temporary storage for raw disk blocks that shouldn't get tremendously large.  
  
`hardware_system_memory_cached_kilobytes`

|

Gauge

|

In-memory cache for files read from the disk. This doesn't include
`SwapCached`.  
  
`hardware_system_memory_mem_available_kilobytes`

|

Gauge

|

An estimate of how much memory is available for starting new applications,
without swapping.  
  
`hardware_system_memory_mem_free_kilobytes`

|

Gauge

|

Sum of `LowFree` \+ `HighFree`.  
  
`hardware_system_memory_mem_total_kilobytes`

|

Gauge

|

Total usable RAM (physical RAM minus a few reserved bits and the kernel binary
code).  
  
`hardware_system_memory_shared_mem_kilobytes`

|

Gauge

|

Amount of memory consumed in file systems whose contents reside in virtual
memory.  
  
`hardware_system_memory_swap_free_kilobytes`

|

Gauge

|

Total amount of swap space unused.  
  
`hardware_system_memory_swap_total_kilobytes`

|

Gauge

|

Total amount of swap space available.  
  
`hardware_system_network_eth0_bytes_in_bytes`

|

Counter

|

Number of bytes of data received by the interface.  
  
`hardware_system_network_eth0_bytes_out_bytes`

|

Counter

|

Number of bytes of data transmitted by the interface.  
  
`hardware_system_network_lo_bytes_in_bytes`

|

Counter

|

Number of bytes of data received by the interface.  
  
`hardware_system_network_lo_bytes_out_bytes`

|

Counter

|

Number of bytes of data transmitted by the interface.  
  
`hardware_system_vm_page_swap_in`

|

Counter

|

Number of pages the system has swapped in from disk.  
  
`hardware_system_vm_page_swap_out`

|

Counter

|

Number of pages the system has swapped out to disk.  
  
## Hardware Metric Labels

Each hardware metric contains the following labels:

Label

|

Description  
  
|  
  
`group_id`

|

Unique hexadecimal digit string that identifies the project.  
  
`org_id`

|

Unique hexadecimal digit string that identifies the organization.  
  
`process_port`

|

Port on which the process runs.  
  
`disk_name`

|

Human-readable label that identifies the disk.  
  
← Integrate with PagerDutyView and Download MongoDB Logs →

