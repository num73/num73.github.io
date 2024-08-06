# Chapter 1 Introduction to Consistency and Coherence

Designing and evaluating a correct shared memory system requires an architect to understand memory consistency and cache coherence, the two topics of this primer.

## CONSISTENCY

Consistency models define correct shared memory behavior in terms of loads and stores (memory reads and writes), without reference to caches or coherence. Shared memory correctness--that is, which shared memory behaviors are allowed--so that programmer know what to expect anc implemntors know the limits to what they can provide.

Shared memory correctness is specified by a memory consistency model or, more simple, a memory model. The memory model specifies the allowed behavior of multithreaded programs executing with shared memory.For a multithreaded program executing with specific input data, the memory model specifies what values dynamic loads may return and, optionally, what possible final states of the memory are. Unlike single-threaded execution, multiple correct behaviors are usually allowed, making understanding memory consistency models subtle.


> A case of monery consistency:\
> Assume that the Computer Architecture course is originally scheduled to be in Room 152. The day before classes begin, the university registrar decides to move the class to Room 252. The registrar sends an e-mail message asking the website administrator to update the online schedule, and a few minutes later, the registrar sends a text message to all registered students to check the newly updated schedule. It is not hard to imagine a scenario—if, say, the website administrator is too busy to post the update immediately—in which a diligent student receives the text message, immediately checks the online schedule, and still observes the (old) class location Room 152. Even though the online schedule is eventually updated to Room 252 and the registrar performed the “writes” in the correct order, this diligent student observed them in a different order and thus went to the wrong room.

## COHERENCE

Access to stale data (incoherence) is prevented using a coherence protocol, which is a set of rules implemented by the distributed set of actors within a system. Essentially, all of the variants make one processor’s write visible to the other processors by propagating the write to all caches. There are two major classes of coherence protocols. In the first approach, the coherence protocol ensures that writes are propagated to the caches synchronously. In the second approach, the coherence protocol propagates writes to the caches asynchronously, while still honoring the consistency model.

> A case of cache coherence:\
> A student checks the online schedule of courses, observes that the Computer Architecture course is being held in Room 152 (reads the datum), and copies this information into her calendar app in her mobile phone (caches the datum). Subsequently, the university registrar decides to move the class to Room 252, updates the online schedule (writes to the datum) and informs the students via a text message. The student’s copy of the datum is now stale, and we have an incoherent situation. If she goes to Room 152, she will fail to find her class. 




