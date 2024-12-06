# slurmpic

A program to provide status for the compute nodes in a SLURM cluster. The script basically takes the "sinfo" output and presents it in a more organized way.

## Customizations:

The "slurmpic" script has been tested on 2 SLURM clusters, and the only customizations that have been needed are:

1 - set the DEFAULT_PARTITION to be the default partition on your cluster
2 - set GPU_PARTITIONS to be the partitions on your cluster that have GPUs


## Usage:

```console
$ slurmpic --help
slurmpic: Used to display a summary of JHPCE SLURM node usage
Usage: slurmpic [-p|--partition PARTITION] [-a|--all] [-g|--gpu] [-r|--ramstats]
       -p | --partition   Show information for a specific partition.
                          The shared partition is shown by default.
                          Summary statistics are for specified partition(s).
                          Summary statistics exclude nodes in DOWN, DRAIN & RESERVED states.
                          Per-node CPU/RAM used values are for all jobs on that node, from all partitions
       -a | --all         Show information for all partitions.
       -g | --gpu         Show information for all GPU partitions.
       -r | --ramstats    Show extended information about RAM allocation.
                          SYSFREEMEM not precise! It includes buffered/cached memory usage.
```

## Example

```console
$ slurmpic
NODENAME      NODESTATE CPUS_A/T CPU_LOAD  TOT_MEM FREEMEM SYSFREEMEM PARTITIONS
compute-053       mixed   16/ 48    15.71   503 GB  346 GB     370 GB  shared*
compute-054        idle    0/ 48     0.13   503 GB  503 GB     399 GB  shared*
compute-057   allocated   64/ 64     0.41   472 GB   68 GB     399 GB  shared*
compute-058       mixed   60/ 64     6.11   488 GB  104 GB     270 GB  shared*
compute-062        idle    0/ 64     0.29   125 GB  125 GB     438 GB  shared*
. . .

compute-166       mixed    5/ 48     4.70  1007 GB  987 GB     873 GB  shared*
compute-167       mixed    5/ 48     4.77  1007 GB  987 GB     891 GB  shared*
compute-168   allocated   48/ 48    45.00  1007 GB  732 GB     624 GB  shared*
compute-169   allocated   48/ 48    46.76  1007 GB  185 GB     752 GB  shared*
NODENAME      NODESTATE CPUS_A/T CPU_LOAD  TOT_MEM FREEMEM SYSFREEMEM PARTITIONS
Total Cores:   3408 |Alloc Cores:   2185 |Idle Cores:   1223 |Core Usage: % 64
Total RAM: 41692 GB |Alloc RAM: 18585 GB |Free RAM: 23107 GB |RAM Usage:  % 44

$ slurmpic -g -p gpu
NODENAME      NODESTATE CPUS_A/T CPU_LOAD  TOT_MEM FREEMEM SYSFREEMEM  GPUS  PARTITIONS
compute-117       mixed    2/ 24     3.70   376 GB   26 GB     152 GB  3/ 3 gpu
compute-123       mixed    6/ 40     4.77   754 GB  354 GB     498 GB  4/ 4 gpu
compute-126       mixed    9/ 24    11.65   503 GB  123 GB     215 GB  4/ 4 gpu
compute-128    RESERVED    1/ 24    21.49   503 GB  103 GB      98 GB  4/ 4 gpu
compute-170    RESERVED    0/ 24     0.17  1007 GB 1007 GB    1001 GB  0/ 2 gpu
compute-171    RESERVED    3/ 24     3.06   995 GB  545 GB     600 GB  3/ 4 gpu
compute-172       mixed   16/ 24    17.67   995 GB  835 GB     748 GB  4/ 4 gpu
compute-173       mixed   10/ 24    10.59   995 GB  615 GB     307 GB  4/ 4 gpu
NODENAME      NODESTATE CPUS_A/T CPU_LOAD  TOT_MEM FREEMEM SYSFREEMEM PARTITIONS
Total Cores:    208 |Alloc Cores:     47 |Idle Cores:    161 |Core Usage: % 22
Total RAM:  6131 GB |Alloc RAM:  2520 GB |Free RAM:  3611 GB |RAM Usage:  % 41
Total GPUs:  29  | Total GPUs Used:  26
```
And a screenshot showing output with colors...

<img width="485" alt="Screenshot 2024-12-06 at 9 03 45 AM" src="https://github.com/user-attachments/assets/068a7659-07ea-41c4-811f-daeb3238525d">
