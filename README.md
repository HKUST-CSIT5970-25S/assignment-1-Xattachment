[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: QIAN Qixin
### Student Id: 21087207
### Email: qqianac@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > Measurement software: Ubuntu 22.04 via the Phoronix Test Suite.
    > Used phoronix-test-suite benchmark 2502229-NE-CPUTEST1371 without setting parameters.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |Compression Rating: 3689 MIPS,Depression Rating: 3095 MIPS|Ramspeed: 10581(add),10678.59(copy),9907.11(scale),10642.41(triad)|
    | `t2.medium`|Compression Rating: 10054 MIPS,Depression Rating: 5853 MIPS|Ramspeed: 19547.23(add),19790.74(copy),17300.29(scale),20611.8(triad)|
    | `c5d.large`|Compression Rating: 7895 MIPS,Depression Rating: 5250 MIPS|Ramspeed: 14398.28(add),13968.11(copy),13749.27(scale),14197.5(triad)|

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |  4070          | min/avg/max/mdev 0.233/0.353/0.781/0.154|
    | `m5.large` - `m5.large`   |  4960          | min/avg/max/mdev 0.160/0.217/0.688/0.156|
    | `c5n.large` - `c5n.large` |  4940          | min/avg/max/mdev 0.102/0.109/0.134/0.009|
    | `t3.medium` - `c5n.large` |  4740          | min/avg/max/mdev 0.583/0.640/0.840/0.084|
    | `m5.large` - `c5n.large`  |  4960          | min/avg/max/mdev 0.572/0.613/0.935/0.107|
    | `m5.large` - `t3.medium`  |  4820          | min/avg/max/mdev 0.134/0.200/0.703/0.167|

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |465             |min/avg/max/mdev 61.397/61.403/61.420/0.006|
    | N. Virginia - N. Virginia |4790            |min/avg/max/mdev 0.121/0.136/0.162/0.010|
    | Oregon - Oregon           |4610            |min/avg/max/mdev 0.167/0.187/0.252/0.028|
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
