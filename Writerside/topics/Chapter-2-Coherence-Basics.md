# Chapter 2 Coherence Basics

## 2.1 BASELINE SYSTEM MODEL

All cores can perform loads and stores to all (physical) addresses. The multicore processor chip consists of multiple single-threaded cores, each of which has its own private data cache, and a last-level cache (LLC) that is shared by all cores. The cores and the LLC communicate with each other over an interconnection network. The LLC, despite being on the processor chip, is logically a "memory-side cache" and thus does not introduce another level of coherence issues. The LLC is logically just in front of the memory and serves to reduce the average latency of memory access and increase the memory's effective bandwidth. The LLC also serves as an on-chip memory controller.

<img src="image-20240813104308944.png" alt="image-20240813104308944" style="zoom:50%;" />

## 2.2 THE PROBLEM: HOW INCOHERENCE COULD POSSIBLY OCCUR

The possibility of incoherence arises only because of one fundamental issue: **there exist multiple actors with access to caches and memory.**

The table illustrates a simple example of incoherence. The store from Core 1 has not been made visible to Core 2 and consequently C2 is stuck in the while loop. The  cache coherence protocol is implemented to prevent incoherence.

![image-20240813105228693](image-20240813105228693.png)

## 2.3 THE CACHE COHERENCE INTERFACE

A coherence protocol must ensure that writes are made visible to all processors.

As the picture illustrated. The processor cores interact with the coherence protocol through a coherence interface that provides two methods: (1) a read-request method; and (2) a write-request method.

![image-20240813110837419](image-20240813110837419.png)

We classify the coherence protocols into two categories based on the nature of
their coherence interfaces:

1. **Consistency-agnostic coherence**. In the first category, a write is made visible to all other cores before returning.
2. **Consistency-directed coherence.** In the second, more-recent category, writes are propagated asynchronously—a write can thus return before it has been made visible to all processors, thus allowing for stale values (in real time) to be observed.

## 2.4 (CONSISTENCY-AGNOSTIC) COHERENCE INVARIANTS
**Coherence invariants**

1. **Single-Write, Multiple-Read(SWMR) Invariant.** For any memory location A, at any given time, there exists only a single core that may write to A (and can also read it) or some number of cores that may only read A. (Another way to view this definition is to consider, for each memory location, that the memory location’s lifetime is divided up into epochs. In each epoch, either a single core has read-write access or some number of cores (possibly zero) have read-only access.)
2. **Data-Value Invariant.** The value of the  memory location at the start of an epoch is the same as the value of memory location at the end of the its last read-write epoch.

![image-20240815132147605](image-20240815132147605.png)

### 2.4.1 MAINTAINING THE COHERENCE INVARIANTS

If a core wants to read a memory location, it sends messages to the other cores to obtain the current value of the memory location and to ensure that no other cores have cached copies of the memory location in a read-write state. These messages end any active read-write epoch and begin a read-only epoch. If a core wants to write to a memory location, it sends messages to the other cores to obtain the current value of the memory location, if it does not already have a valid read-only cached copy, and to ensure that no other cores have cached copies of the memory location in either read-only or read-write states. These messages end any active read-write or read-only epoch and begin a new read-write epoch.

### 2.4.2 THE GRANULARITY OF COHERENCE

In practice, the SWMR invariant is likely to be that, for any block of memory, there is either a single writer or some number of readers.