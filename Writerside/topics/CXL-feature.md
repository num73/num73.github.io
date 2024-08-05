# CXL Features

## Overview
CXL is a dynamic multi-protocol technology designed to support accelerators and
memory devices. CXL provides a rich set of protocols that include I/O semantics similar
to PCIe (i.e., CXL.io), caching protocol semantics (i.e., CXL.cache), and memory access
semantics (i.e., CXL.mem) over a discrete or on-package link. CXL.io is required for
discovery and enumeration, error reporting, P2P accesses to CXL memory1 and host
physical address (HPA) lookup. CXL.cache and CXL.mem protocols may be optionally
implemented by the particular accelerator or memory device usage model. An
important benefit of CXL is that it provides a low-latency, high-bandwidth path for an
accelerator to access the system and for the system to access the memory attached to
the CXL device. The figure is a conceptual diagram that shows a device attached to a
Host processor via CXL.

<img src="CXL-3.jpg" alt="Figure 1-1" />

## Features
CXL technology architecture consists of three main components :
1. **CXL Devices**: Devices that are compatible with the CXL interface can include processors, accelerators such as Graphics Processing Units (GPUs), and Smart Storage Devices;
2. **CXL Switch**: The switch enables communication between devices that support CXL. The switch can be external or embedded, allowing for more complex topologies;
3. **CXL Memory**: CXL memory devices support the CXL protocol for the efficient sharing of System memory.

CXL includes several key features that make it an attractive technology for high-performance computing in the data center:
1. CXL provides high bandwidth and low latency for data transfers, which is critical for data-intensive workloads such as AI, machine learning, and big data analytics.
2. CXL enables memory expansion, which allows systems to scale up memory capacity without adding additional memory channels.
3. CXL supports coherent memory access, which enables multiple processors to access shared memory in a coherent manner. Finally, CXL provides cache coherence, which ensures that all processors have a consistent view of the data in the cache.
4. CXL technology supports memory semantics, enabling devices to share memory through the CXL interface.

CXL offers several advantages over other interconnect technologies in the data center:
1. CXL provides significantly higher bandwidth and lower latency than other interconnect technologies, such as Ethernet or InfiniBand;
2. CXL enables memory expansion, which can significantly improve the performance of memory-intensive workloads;
3. CXL supports coherent memory access, which enables multiple processors to access shared memory in a coherent manner without the need for additional hardware;
4. CXL provides cache coherence, which ensures that all processors have a consistent view of the data in the cache, which can reduce the likelihood of data inconsistencies and errors.  

The CXL standard supports a variety of use cases via three protocols: CXL.io, CXL.cache, and CXL.memory:
1. **CXL.io:** This protocol is functionally equivalent to the PCIe protocol—and utilizes the broad industry adoption and familiarity of PCIe. As the foundational communication protocol, CXL.io is versatile and addresses a wide range of use cases.
2. **CXL.cache:** This protocol, which is designed for more specific applications, enables accelerators to efficiently access and cache host memory for optimized performance.
3. **CXL.memory:** This protocol enables a host, such as a processor, to access device-attached memory using load/store commands.

The protocols used to interconnect devices and hosts are as follows:
1. Type 1 Devices: CXL.io + CXL.cache
2. Type 2 Devices: CXL.io + CXL.cache + CXL.memory
3. Type 3 Devices: CXL.io + CXL.memory

## Reference:
[1]CXL-3.1-Specification 

[2]Nag, S. N. (2023). "CXL (Compute Express Link) Technology." Journal of Computer and Communications 11(06): 94-102.
	
