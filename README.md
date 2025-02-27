[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: CAI, Huaiyu
### Student Id: 21139725
### Email: hcaiai@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > Your answer goes here. I used Phoronix Test Suite (PTS) to completed CPU performance and memory performance testings. For CPU testings, I utilize pts/compress-7zip, and forcusing on Integer Copy Test, which best reflects basic memory performance as well as copy is the most fundamental memory operation. Using auto-selection of test data size prevents memory pressure, 3 rounds ensure result reliability, batch mode ensures consistent testing conditions. The results of means how many MB integer data per second the system can copy, reflecting the data transfer capability of the memory subsystem.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` | Compre: 3699MIPS; Decompre: 3099MIPS | Copy(int): 10935.33 MB/s; Random Write: 144.842 MB/s; Random Read: 2561.599 MB/s |
    | `t2.medium`  | Compre: 9835 MIPS; Decompre: 5786 MIPS | Copy(int): 19260.19 MB/s; Random Write: 147.730 MB/s; Random Read:  58745.767 MB/s|
    | `c5d.large` | Compre: 7552 MIPS; Decompre:  4896 MIPS| Copy(int): 13801.99 MB/s; Random Write: 188.215 MB/s; Random Read:  80723.445 MB/s|

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | 3790 | 0.281 |
    | `m5.large` - `m5.large`   | 3120 | 0.546 |
    | `c5n.large` - `c5n.large` | 4930 | 0.156 |
    | `t3.medium` - `c5n.large` | 2240 | 0.760 |
    | `m5.large` - `c5n.large`  | 4110 | 0.391 |
    | `m5.large` - `t3.medium`  | 1690 | 0.971 |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | 3190 | 61.580 |
    | N. Virginia - N. Virginia | 4860 | 0.248 |
    | Oregon - Oregon           | 4960 | 0.145 |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
