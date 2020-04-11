# Mutlithreading


| General	| Concurrency Concurrency control |
| ------------- | ------------- |
| Process calculus	| CSP / CCS / ACP / LOTOS / π-calculus / Ambient calculus / API-Calculus / PEPA / Join-calculus |
| Classic problems |	[ABA problem](#aba-problem) / [Cigarette smokers problem](#cigarette-smokers-problem) / [Deadlock](#deadlock) / [Dining philosophers problem](#dining-philosophers-problem) / [Producer consumer problem](#producer-consumer-problem) / [Race condition](#race-condition) / [Readers–writers problem](#readers-writers-problem) / [Sleeping barber problem](#sleeping-barber-problem) |

Source: [Wikipedia](https://en.wikipedia.org/wiki/Template:Concurrent_computing)

## Process calculus

In Progress..

## Classic problems

### [ABA Problem](https://en.wikipedia.org/wiki/ABA_problem)
In multithreaded computing, the ABA problem occurs during synchronization, when a location is read twice, has the same value for both reads, and "value is the same" is used to indicate "nothing has changed". However, another thread can execute between the two reads and change the value, do other work, then change the value back, thus fooling the first thread into thinking "nothing has changed" even though the second thread did work that violates that assumption.

### [Cigarette smokers problem](https://en.wikipedia.org/wiki/Cigarette_smokers_problem)
Assume a cigarette requires three ingredients to make and smoke: tobacco, paper, and matches. There are three smokers around a table, each of whom has an infinite supply of one of the three ingredients — one smoker has an infinite supply of tobacco, another has paper, and the third has matches.

There is also a non-smoking agent who enables the smokers to make their cigarettes by arbitrarily (non-deterministically) selecting two of the supplies to place on the table. The smoker who has the third supply should remove the two items from the table, using them (along with their own supply) to make a cigarette, which they smoke for a while. Once the smoker has finished his cigarette, the agent places two new random items on the table. This process continues forever.

### [Deadlock](https://en.wikipedia.org/wiki/Deadlock)
In concurrent computing, a deadlock is a state in which each member of a group is waiting for another member, including itself, to take action, such as sending a message or more commonly releasing a lock.[1] Deadlock is a common problem in multiprocessing systems, parallel computing, and distributed systems, where software and hardware locks are used to arbitrate shared resources and implement process synchronization.

### [Dining philosophers problem](https://en.wikipedia.org/wiki/Dining_philosophers_problem)
In computer science, the dining philosophers problem is an example problem often used in concurrent algorithm design to illustrate synchronization issues and techniques for resolving them.

Five silent philosophers sit at a round table with bowls of spaghetti. Forks are placed between each pair of adjacent philosophers.

Each philosopher must alternately think and eat. However, a philosopher can only eat spaghetti when they have both left and right forks. Each fork can be held by only one philosopher and so a philosopher can use the fork only if it is not being used by another philosopher. After an individual philosopher finishes eating, they need to put down both forks so that the forks become available to others. A philosopher can take the fork on their right or the one on their left as they become available, but cannot start eating before getting both forks.

### [Producer consumer problem](https://en.wikipedia.org/wiki/Producer%E2%80%93consumer_problem)
In computing, the producer–consumer problem[1][2] (also known as the bounded-buffer problem) is a classic example of a multi-process synchronization problem. The problem describes two processes, the producer and the consumer, who share a common, fixed-size buffer used as a queue. The producer's job is to generate data, put it into the buffer, and start again. At the same time, the consumer is consuming the data (i.e., removing it from the buffer), one piece at a time. The problem is to make sure that the producer won't try to add data into the buffer if it's full and that the consumer won't try to remove data from an empty buffer.

### [Race condition](https://en.wikipedia.org/wiki/Race_condition)
A race condition or race hazard is the behavior of an electronics, software, or other system where the system's substantive behavior is dependent on the sequence or timing of other uncontrollable events. It becomes a bug when one or more of the possible behaviors is undesirable.

### [Readers writers problem](https://en.wikipedia.org/wiki/Readers%E2%80%93writers_problem) 
In computer science, the readers-writers problems are examples of a common computing problem in concurrency. There are at least three variations of the problems, which deal with situations in which many threads (small processes which share data) try to access the same shared resource at one time. Some threads may read and some may write, with the constraint that no process may access the shared resource for either reading or writing while another process is in the act of writing to it. (In particular, we want to prevent more than one thread modify the shared resource simultaneity and allowed for two or more readers to access the shared resource at the same time). A readers-writer lock is a data structure that solves one or more of the readers-writers problems.

### [Sleeping barber problem](https://en.wikipedia.org/wiki/Sleeping_barber_problem) 
In computer science, the sleeping barber problem is a classic inter-process communication and synchronization problem between multiple operating system processes. The problem is analogous to that of keeping a barber working when there are customers, resting when there are none, and doing so in an orderly manner.

The analogy is based upon a hypothetical barber shop with one barber. The barber has one barber's chair in a cutting room and a waiting room containing a number of chairs in it. When the barber finishes cutting a customer's hair, he dismisses the customer and goes to the waiting room to see if there are others waiting. If there are, he brings one of them back to the chair and cuts their hair. If there are none, he returns to the chair and sleeps in it.

Each customer, when they arrive, looks to see what the barber is doing. If the barber is sleeping, the customer wakes him up and sits in the cutting room chair. If the barber is cutting hair, the customer stays in the waiting room. If there is a free chair in the waiting room, the customer sits in it and waits their turn. If there is no free chair, the customer leaves.
