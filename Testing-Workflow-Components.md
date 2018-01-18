The software test program components identified in the __Introduction__ are described individually in this section.

## Platforms

To achieve the goal of enabling software applications to become performant on variety of systems, software testing must take place on a wide range of architectures. Integral to this effort at Sandia is the collection of machines referred to as the Heterogeneous Advanced Architecture Platforms or HAAPs ( https://snl-wiki.sandia.gov/display/HAAPs ). A subset of these machines are identified in Table 2.1 as the primary (P) test platforms, while other machines with similar characteristics are identified as alternate (or secondary (S) ) test machines that can be used in the event of maintenance or other outages of the primary. The HAAPs link above (scroll to the Platforms section) is the official specifications for these machines. The Platforms table on the HAAPs link contains specifications for both the CPUs and the GPUs (accelerators) when present on a particular platform. Note, the information in Table 2.1 is a subset of that presented in the HAAPs table. The last column designates the network on which a particular machine exists (OHPC – Open Network, SRN – Sandia Restricted Network).

[ decide if summary needed or not: A summary of these machines in Attachment M provides further details. ]


<h4>Table 2.1: Kokkos Test Platforms and Characteristics</h4>
  
 Platform | Category | CPU Type | Nodes/Cores | Accelerator Type | Num GPUs | Network
 :--- |:--- |:--- |:--- |:--- |:--- |:---
`Apollo`| P | ? |  ?  |  None |  NA  | Local/OHPC?
`Bowman`| P | Knights Landing |  32/-  |  None |  NA  | OHPC 
`Ellis`| S | Knights Landing |  32/-  |  None |  NA  | SRN
`Hansen`| S | Intel  Xeon Haswell E5-2698 |  3/16  |  None |  NA  | OHPC
`Kokkos_Dev`| P | x86 |  20  |  None |  NA  | SRN
`Ride`| S | P8-Tuleta, P8-Firestone, P8-Garrison  |  4/10, 11/10, 8/10  |  NVIDIA Tesla |  4 K40, 11 K80, 8 P100  | SRN
`Shepard`| P | Intel Xeon Haswell E5-2698  |  36/16  |  None |  NA  | SRN
`Sullivan`| S | Cavium ThunderX v1, v2 |  20, 2  |  None |  NA  | OHPC
`Local Macs`| S | ? | 4 or 8  |  None |  NA  | Local
`White`| P | P8-Tuleta, P8-Firestone, P8-Garrison  |  9/10, 8/8, 8/8  |  NVIDIA Tesla |  7 K40, 7 K80, 8 P100  |  32  |  None |  NA | OHPC
`Others from Jenkins List`| P | ? |  *  |  None |  NA  | OHPC


## Batch Queues

Examining the list of machines in Table 2.1, one can see that a wide range of hardware types constitute our collection of test beds. Some platforms have several different types of processors, including CPUs and GPUs. In order to access a homogeneous collection of nodes when runs are made on one these machines, several queues have been setup, one for each hardware/architecture type. It is necessary to load the proper environment for these nodes and use a batch submission script that selects the desired queue explicitly. More details are provided in the section that discusses the test scripts used for all Kokkos testing.

## Computer Accounts

Sandia computing machines are connected to various networks and require access permissions be obtained through an account control system, normally WebCARS. Each of the machines listed above requires an account be obtained through WebCARS, except for Apollos and Kokkos-dev. Machines identified as Local are normally personal hardware of various kinds that are issued to (Kokkos team) staff members. Accounts on Kokkos-dev may be obtained through permission of Kokkos project leads and the assistance of CSRI CSU staff members. The Kokkos-dev and primary machines are required accounts for most testing, but most especially for promotion testing (described below). It is recommended that Kokkos team members obtain accounts on all the machines listed in Table 2.1.
