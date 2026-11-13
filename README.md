# OS Laboratory Activity 3
## Multilevel Queue and Real-Time CPU Scheduling
 
## Student Information
- Name: Princess Nashema M. Macasero
- Course and Section: BS Computer Applications | B186
- Instructor: Maria Fe P. Bahinting
- Date Submitted: November 13, 2026
 
## I. Introduction

This laboratory activity focuses on implementing and understanding three CPU scheduling algorithms: Multilevel Queue (MLQ), Rate Monotonic Scheduling (RMS), and Earliest Deadline First (EDF).

The activity uses Python to simulate how the CPU handles different processes and periodic tasks. It also uses Gantt charts to show the execution order of tasks. Through this activity, we can understand how scheduling algorithms assign priorities, manage CPU time, and check whether tasks finish before their deadlines.
 
## II. Objectives

1. Explain the operation of Multilevel Queue, RMS, and EDF scheduling.
2. Implement MLQ scheduling using Round Robin and FCFS.
3. Implement preemptive RMS and EDF simulations in Python.
4. Generate and interpret Gantt charts of process/task execution.
5. Calculate CPU utilization, waiting time, turnaround time, and deadline compliance.
6. Create and manage a GitHub repository with source code and documentation.
 
## III. Scheduling Algorithms

## **1. Multilevel Queue Scheduling (MLQ)**

Multilevel Queue Scheduling divides processes into different queues based on their categories. In this activity, there are two queues:

-  Queue 1: Handles interactive processes using Round Robin with a time quantum of 2 ms.

- Queue 2: Handles batch processes using First Come, First Served (FCFS).

Queue 1 has higher priority than Queue 2. If a Queue 1 process becomes ready while a Queue 2 process is running, the Queue 2 process is interrupted and resumes later.

## **2. Rate Monotonic Scheduling (RMS)**

RMS is a fixed-priority preemptive scheduling algorithm used for periodic real-time tasks. The task with the shortest period receives the highest priority.

For this activity, the priority order is:

1. T1 – Highest priority (4 ms period)

2. T2 – Second priority (5 ms period)

3. T3 – Lowest priority (10 ms period)

A higher-priority task can interrupt a lower-priority task when it becomes ready.

## **3. Earliest Deadline First (EDF)**

EDF is a dynamic-priority preemptive scheduling algorithm. It selects the ready task with the earliest absolute deadline.

The absolute deadline is calculated using:

Absolute Deadline = Release Time + Relative Deadline

Unlike RMS, EDF does not have a permanent priority order. The priority changes depending on the deadlines of the available tasks.
 
### IV. Program Implementation

## **1. Multilevel Queue Scheduling**

The MLQ program was implemented in Python using the deque module to manage the ready queues.

The program separates processes into Queue 1 and Queue 2. Queue 1 uses Round Robin with a 2 ms time quantum, while Queue 2 uses FCFS. The program also checks the remaining burst time of each process and generates a Gantt chart showing the execution sequence.

After execution, it calculates the completion time, turnaround time, waiting time, and their averages.

## **2. Rate Monotonic Scheduling**

The RMS program was implemented using Python lists to store task information and their generated instances.

Each task has an execution time, period, and relative deadline. The program generates new task instances based on their periods and assigns priorities according to the shortest period.

The CPU checks the ready tasks every 1 ms and selects the task with the highest fixed priority. It also generates a Gantt chart, calculates CPU utilization, and checks whether each task instance meets its deadline.

## **3. Earliest Deadline First**

The EDF program was implemented using Python to manage periodic task instances and their absolute deadlines.

Every 1 ms, the program checks the ready tasks and selects the one with the earliest absolute deadline. If a task with an earlier deadline becomes ready, it can interrupt the currently running task.

The program generates a Gantt chart and displays the completion time and deadline status of each task instance. It also calculates CPU utilization and checks whether the task set passes the classical EDF utilization test.
 
### V. Test Data

## **1. MLQ Test Data**

| Process | Arrival Time | Burst Time | Queue |
| :-----: | :----------: | :--------: | :---: |
| P1      | 0            | 5          | 1     |
| P2      | 1            | 4          | 1     |
| P3      | 0            | 6          | 2     |
| P4      | 2            | 3          | 2     |
| P5      | 3            | 2          | 1     |

- Queue 1: Round Robin
- Queue 2: FCFS
- Time Quantum: 2 ms
- Queue 1 has higher priority than Queue 2.

## **2. RMS Test Data**

| Task | Execution Time (C) | Period (T) | Deadline (D) |
| :--: | :----------------: | :--------: | :----------: |
| T1   | 1 ms               | 4 ms       | 4 ms         |
| T2   | 1 ms               | 5 ms       | 5 ms         |
| T3   | 2 ms               | 10 ms      | 10 ms        |

- Simulation Time: 20 ms
- Scheduling Type: Preemptive
- Priority: Shortest period receives the highest priority.

## **3. EDF Test Data**

| Task | Execution Time (C) | Period (T) | Deadline (D) |
| :--: | :----------------: | :--------: | :----------: |
| T1   | 1 ms               | 4 ms       | 4 ms         |
| T2   | 1 ms               | 5 ms       | 5 ms         |
| T3   | 2 ms               | 10 ms      | 10 ms        |

- Simulation Time: 20 ms
- Scheduling Type: Preemptive
- Priority: Earliest absolute deadline receives the highest priority.
 
### VI. Results and Discussion

## **1. MLQ Scheduling Results**

**Gantt Chart**

| P1 [0-2] | P2 [2-4] | P1 [4-6] | P5 [6-8] |
| P2 [8-10] | P1 [10-11] | P3 [11-17] | P4 [17-20] |

Process Performance

| PID | AT  | BT  | CT  | TAT | WT  |
| :-: | :-: | :-: | :-: | :-- | :-- |
| P1  | 0   | 5   | 11  | 11  | 6   |
| P2  | 1   | 4   | 10  | 9   | 5   |
| P3  | 0   | 6   | 17  | 17  | 11  |
| P4  | 2   | 3   | 20  | 18  | 15  |
| P5  | 3   | 2   | 8   | 5   | 3   |

Performance Metrics

- Average Turnaround Time: 12.0 ms
- Average Waiting Time: 8.0 ms
- CPU Utilization: 100%

The results show that Queue 1 processes received priority over Queue 2 processes. Round Robin allowed the interactive processes to take turns using the CPU, while FCFS handled the batch processes in their arrival order.

All processes completed within the 20 ms execution period. The CPU utilization was 100% because there was no idle time during the simulation. Queue 2 processes had longer waiting times because they had lower priority.

## **2. RMS Results**

Priority Order

T1 > T2 > T3

**Gantt Chart**

| T1 [0-1] | T2 [1-2] | T3 [2-4] | T1 [4-5] | T2 [5-6] | IDLE [6-8] | T1 [8-9] | IDLE [9-10] | T2 [10-11] | T3 [11-12] | T1 [12-13] | T3 [13-14] | IDLE [14-15] | T2 [15-16] | T1 [16-17] | IDLE [17-20] |

Task Instance Results

| Task | Release | Deadline | Completion | Status |
| :--: | :-----: | :------: | :--------: | :----: |
| T1   | 0       | 4        | 1          | MET    |
| T2   | 0       | 5        | 2          | MET    |
| T3   | 0       | 10       | 4          | MET    |
| T1   | 4       | 8        | 5          | MET    |
| T2   | 5       | 10       | 6          | MET    |
| T1   | 8       | 12       | 9          | MET    |
| T2   | 10      | 15       | 11         | MET    |
| T3   | 10      | 20       | 14         | MET    |
| T1   | 12      | 16       | 13         | MET    |
| T2   | 15      | 20       | 16         | MET    |
| T1   | 16      | 20       | 17         | MET    |

Performance Metrics

- CPU Utilization: 65.0%
- RMS Sufficient Utilization Bound: 77.98%
- Sufficient-Bound Test: PASS
- Deadline Misses: 0

The results show that T1 receives the highest priority because it has the shortest period. T2 follows, while T3 has the lowest priority. The CPU becomes idle when there are no ready tasks.

The CPU utilization is 65%, which is below the RMS sufficient utilization bound of 77.98%. The program passed the utilization-bound test, and all 11 task instances successfully completed before their deadlines.

## **3. EDF Results**

**Gantt Chart**

| T1 [0-1] | T2 [1-2] | T3 [2-4] | T1 [4-5] | T2 [5-6] | IDLE [6-8] | T1 [8-9] | IDLE [9-10] | T2 [10-11] | T3 [11-12] | T1 [12-13] | T3 [13-14] | IDLE [14-15] | T2 [15-16] | T1 [16-17] | IDLE [17-20] |

Task Instance Results

| Task | Release | Deadline | Completion | Status |
| :--: | :-----: | :------: | :--------: | :----: |
| T1   | 0       | 4        | 1          | MET    |
| T2   | 0       | 5        | 2          | MET    |
| T3   | 0       | 10       | 4          | MET    |
| T1   | 4       | 8        | 5          | MET    |
| T2   | 5       | 10       | 6          | MET    |
| T1   | 8       | 12       | 9          | MET    |
| T2   | 10      | 15       | 11         | MET    |
| T3   | 10      | 20       | 14         | MET    |
| T1   | 12      | 16       | 13         | MET    |
| T2   | 15      | 20       | 16         | MET    |
| T1   | 16      | 20       | 17         | MET    |

Performance Metrics

- CPU Utilization: 65.0%
- Classical EDF Utilization Test: PASS
- Deadline Misses: 0

The results show that EDF successfully scheduled all task instances based on their absolute deadlines. Tasks with earlier deadlines were given priority, and all 11 task instances completed before their deadlines.

The CPU utilization is 65%, which is below 100%. Therefore, the task set passed the classical EDF utilization test under the assumptions used in the activity.
 
### VII. Algorithm Comparison

| Criteria            | MLQ                     | RMS                      | EDF                            |
| :-----------------: | :---------------------: | :----------------------: | :----------------------------: |
| Scheduling Basis    | Queue priority          | Task period              | Absolute deadline              |
| Priority Assignment | Fixed queue priority    | Fixed task priority      | Dynamic task priority          |
| Scheduling Type     | Depends on queue policy | Preemptive               | Preemptive                     |
| Main Application    | Process classification  | Periodic real-time tasks | Deadline-based real-time tasks |
| Deadline Monitoring | Not inherent            | Yes                      | Yes                            |

Discussion: 

MLQ focuses on dividing processes into different queues based on their categories. Each queue can use a different scheduling algorithm.

RMS assigns fixed priorities based on task periods. Tasks with shorter periods always have higher priority.

EDF assigns priorities based on absolute deadlines. The priority can change depending on the deadlines of ready tasks.

Among the three algorithms, MLQ is useful for managing different types of processes, while RMS and EDF are more suitable for real-time scheduling. RMS is simpler because its priorities remain fixed, while EDF is more flexible because it considers the deadlines of ready tasks.

For this particular dataset, RMS and EDF produced identical Gantt charts, CPU utilization, and deadline results. However, their priority assignment methods are different.
 
### VIII. Guide Questions

1. What is the main difference between Multilevel Queue and Multilevel Feedback Queue scheduling?

- Multilevel Queue uses fixed queues, and processes cannot move between them. Multilevel Feedback Queue allows processes to move between queues depending on their behavior and CPU usage.

2. Why does MLQ use different scheduling algorithms for different process queues?

- MLQ uses different algorithms because each queue handles a different type of process. For example, interactive processes use Round Robin, while batch processes use FCFS.

3. How does RMS determine which task receives the CPU first?

- RMS gives the highest priority to the task with the shortest period. If multiple tasks are ready, the task with the highest fixed priority executes first.

4. Why is RMS considered a fixed-priority scheduling algorithm?

- RMS is considered fixed-priority because the priority of each task is determined by its period and does not change during execution.

5. How does EDF determine which task should execute next?

- EDF selects the ready task with the earliest absolute deadline. The task that needs to finish sooner receives the CPU first.

6. Why is EDF considered a dynamic-priority scheduling algorithm?

- EDF is dynamic because task priorities can change depending on their absolute deadlines. Every time the scheduler checks the ready tasks, it selects the one with the earliest deadline.

7. What happens when a newly released task has an earlier deadline than the currently running task under EDF?

- The newly released task receives higher priority and can interrupt the currently running task. The interrupted task can continue later when it becomes the highest-priority ready task.

8. Why is CPU utilization important in real-time scheduling?

- CPU utilization shows how much of the processor's available time is being used. It helps determine whether the processor has enough capacity to execute the required tasks before their deadlines.

9. Can a task set with CPU utilization below 100% still miss a deadline? Explain the conditions under which this may happen.

- Yes. A task set can still miss a deadline even if CPU utilization is below 100%. This may happen when tasks have different deadline requirements, execution times, or scheduling priorities. Having unused CPU time does not always guarantee that every task will finish on time.

10. Which algorithm would you recommend for periodic real-time tasks, RMS or EDF? Justify your answer.

- I would recommend EDF because it considers the absolute deadlines of tasks when assigning priorities. It is flexible and can schedule periodic tasks based on which deadline comes first. However, RMS is also useful because it has a simpler and fixed priority system.

### IX. Conclusion

Through this laboratory activity, I learned how different CPU scheduling algorithms manage processes and tasks. I was able to understand how MLQ uses separate queues with different scheduling policies, how RMS assigns fixed priorities based on task periods, and how EDF selects tasks based on their absolute deadlines.

I also learned how to implement scheduling algorithms using Python, generate Gantt charts, calculate CPU utilization, and check whether tasks meet their deadlines.

The activity helped me understand the importance of CPU scheduling in operating systems, especially when handling multiple processes and real-time tasks. It also gave me experience in using GitHub to organize and document my programming activities.


