# IOPMP Charter

Security of a platform is an ever-present issue, and a fundamental requirement of security is memory 
isolation. CPUs are not the only agents able to access memory, however. Other bus masters in a platform, 
e.g., DMA or GPU, can do as well. While a RISC-V hart may have a PMP/ePMP, SMPU, or MMU to control its 
accesses, a mechanism is also needed to control accesses from those bus masters.

The protection mechanisms inside a hart, e.g., PMP/ePMP, SMPU, or MMU, create memory isolations according 
to a specific hart and its mode. These mechanisms check every access issued from the hart. However, the other 
bus masters do not usually have any similar checking mechanism. Thus, these bus masters can access anywhere. 
A bus master might need access to regions belonging to multiple harts or multiple modes or need access to only 
a subset of the region belonging to a hart\xe2\x80\x99s mode. That is, the memory view of a bus master should 
be orthogonal to that of a hart. The IOPMP will associate a bus master to the corresponding regions independently 
from any hart. Thus, the Memory Domain was introduced as the memory view of a bus master. The IOPMP is also designed 
for a system not implementing an MMU, such as MCU or IoT with limited memory. Consequently, the current RISC-V 
memory protection mechanism cannot fully cover the IOPMP\xe2\x80\x99s targets.

A software solution has been proposed and implemented for RISC-V that requires each memory transfer request checked 
by higher-privileged software before being performed. However, it suffers from longer latency and is challenging 
to extend to complex bus masters, e.g., GPU or DSP, which can take a program as an input. This TG will define the 
IOPMP, which checks transactions on the fly and stop those with any violations.

The IOPMP Task Group will deliver an IOPMP architectural specification as a reference for the developers of 
a new project or an extension of a legacy project. Platforms are diversified and have different latency, 
performance, area, capacity, and portability requirements. The architectural definition will cover platforms 
with a range of scales, bus masters, and bus protocols. They are considered not only for new-designed systems 
but also for enabling the integration of legacy platforms into the RISC-V ecosystem. Consequently, the Task 
Group will define several options, standard models, and extensions to accommodate different requirements. 
Due to a certain number of options and models provided, we need to take portability into consideration. 
Besides the configuration structure under discussion, we will also provide a procedure of standard model discovery.

In the TEE Task group, we have already discussed and will incorporate:

1. how to associate a bus master with a set of rules,
2. how to protect the rules and related settings,
3. the atomicity and consistency issue when programming an IOPMP, and
4. the standard procedure for model discovery.

The IOPMP will complete this existing foundation by incorporating the above in a specification and further defining:

* register definitions (in the MMIO space),
* reset process,
* reactions to an access violation (including the AIA supporting),
* additional usage cases, and
* analysis of IOPMP attacks.

Besides the specification, we will provide a simulator. If the resource is available, we will also provide 
test cases and the reference code for a security monitor manipulating the IOPMPs.

We are aware of some related items not included in this version. If we receive the requests and agree, we 
may cover the following items in the future version:

* the error handling of speculative accesses,
* the mitigation of denial-of-service and side-channel attacks,
* supporting NoC,
* the interactions with the caches and the cache manipulation operations,
* programming the source ID, or
* supporting multiple VMs in a hart with different permissions.
