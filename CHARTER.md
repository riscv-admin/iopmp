Security of a platform is an ever-present issue, and a fundamental requirement of security is memory isolation. CPUs are not the only agents able to access memory, however. The other types of bus masters in a platform, e.g., DMA or GPU, can do as well. While a RISC-V hart can have PMP/ePMP, SMPU, or MMU to control its accesses, a mechanism is also needed to control accesses from the others.

IOPMP provides access control over accesses to system address space by I/O agents to protect multiple security domains with separate access controls. These access controls are operated directly by software in charge of security, typically running in M-mode.

In the first stage, the IOPMP Task Group will deliver an IOPMP architectural specification for the features requested mostly, including
 (1) how to build domains by associating bus masters with sets of rules for accessing resources, 
 (2) how to protect the rules and related settings,
 (3) the atomicity and consistency issue when programming an IOPMP, 
 (4) register definitions (in the MMIO space),
 (5) reset process, and
 (6) reactions to an access violation (including the AIA supporting).

Besides the specification, we will provide a simulator. If the resource is available, we will also provide test cases and the reference code for M-mode software managing IOPMPs.

We are aware of some related items not covered in the first version. If we receive the requests and agree, we may include the following items in future versions:
- the error handling of speculative accesses,
- the mitigation of denial-of-service and side-channel attacks,
- supporting NoC,
- the interactions with the caches and the cache manipulation operations,
- programming the source ID, or
- supporting multiple VMs in a hart with different permissions.
- 
