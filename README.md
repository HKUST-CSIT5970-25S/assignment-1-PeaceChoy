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

    > I used Phoronix Test Suite (PTS) to completed CPU performance and memory performance testings. 
    > For CPU testings, I utilized pts/compress-7zip to test the ability of compression and decompression in order to test how many thousand instructions the system can process per second, directly reflecting the system's ability to handle complex calculations, as well as comprehensive performance including memory access and data processing. 
    > For memory testings, I utilized pts/ramspeed, and focusing on integer copy, random write and random read testings, as these operations most effectively demonstrate fundamental memory performance and represent essential memory operations. Using auto-selection of test data size prevents memory pressure, 3 rounds ensure result reliability, batch mode ensures consistent testing conditions. For random write and random read operations, I configured them with 128MB data size and 4 threads. These parameters were chosen considering: 128MB data size ensures sufficient workload without overwhelming system memory. 4 threads optimize parallel processing while maintaining system stability. These settings provide a balanced test environment for typical memory operations The results are measured in MB/s, indicating the system's memory bandwidth - the amount of integer data that can be transferred per second, which directly represents the memory subsystem's data transfer capabilities. 
    > For EC2 Network performance testings, I used iperf to complete the whole testings. As for TCP, we set tcp windows equaling to 256KB since it strikes an optimal balance between memory utilization and network performance, making it well-suited for most modern network environments. The results represent the throufhput, which reflects the actual network bandwidth utilization. As for RTT, I used ping testings, beacause it provides a simple and reliable way to evaluate network performance using the ICMP protocol. The results show the average time taken for data packets to travel from source to destination and back, measured in milliseconds (ms). Addiyionally, If instances are operating in different regions, using the public IP. If the same, using the private IP. 

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
