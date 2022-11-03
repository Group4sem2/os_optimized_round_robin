# os_optimized_round_robin
# Idea
The current way in which the Round Robin works is where each process is assigned a fixed time slot in a cyclic way. It is basically the preemptive version of First come First Serve CPU Scheduling algorithm. 
Round Robin CPU Algorithm generally focuses on Time Sharing technique.  The period of time for which a process or job is allowed to run in a pre-emptive method is called time quantum.  Each process or job present in the ready queue is assigned the CPU for that time quantum, if the execution of the process is completed during that time then the process will end else the process will go back to the waiting table and wait for its next turn to complete the execution.
With the current implementation there are many advantages but also some disadvantages, disadvantages is such that suppose there is a ready queue of 500 process waiting to be occupied by the CPU and if the process get the CPU and after a time quantum if the process is just about to finish, that is it only require few milliseconds of the CPU processing to complete the process. It still moves back to the top of the ready queue. Now the task only require few millisecond of CPU process to complete, but it still have to wait for roughly  500 time quantum to again getting the CPU, considering that all the process in the queue require about a time quantum of process time to complete. 

This is the biggest draw back of Round Robin, that is if a process is about to finish but due the time quantum it moves back to the top of the queue again waiting for all the process below to complete. This increases the waiting time of the process. 

If suppose we were able to provide a way to all such process that just require a minute time of CPU process to finish but end up waiting for the whole queue of process to complete, it will drastically improve waiting time of the process hence improving the algorithm. 

To solve the same issue we came up with a simple solution that is to use two queue in the algorithm instead of just one. One queue will act the usual ready queue, the other will act as for the process that were about to finish but were not able to due to the time quantum. 






# WORKING

Let us consider two queue named RQ for ready queue and QQ for Quickly queue, basically its the queue of the process that can finish quickly if CPU is allotted to them.

Let us consider 100 of process having random Burst Time (BT). Let’s keep a pointer P that is point to the queue which is been processed. At first the pointer will be pointing to the RQ and works as usual Round Robin Algorithm, but if suppose it come across such a process whose turn if finished and is about to be moved at the back of RQ we will have a simple check if it’s remaining time quantum is less than the Time Quantum of the Algorithm, if it is, we will move the process into the QQ instead of RQ. After, let’s  N time quantum the pointer moves to the QQ then its start process in the QQ as usual Round Robin Algorithm. And again after M time quantum or if the QQ is empty we will more back to RQ.

Here one important thing is to make sure the the switching time N & M are not too small or not too big, because if its too small the context switching will increase which will slow down the algorithm and increase the space required. And if they are too large it will increase the waiting time which will again slow down the algorithm. 
