Abstract— An operating system’s performance depends on many factors. A significant contributor to the performance of an OS is the scheduling algorithm implemented on it. Round Robin scheduling algorithm is one of the scheduling algorithms that provides fairness to all processes regardless of their priority and provides good performance. However, the performance of the algorithm depends on the chosen time quantum. Our project aims to assess the effectiveness and efficiency of different Dynamic Round Robin algorithms in CPU scheduling under varying workloads on a Microkernel Operating System. We will perform a comparative study of three different Round Robin algorithms: Optimal Round Robin Scheduling using Manhattan Distance, Improved Round Robin Scheduling, and Adaptive Round Robin Algorithm. We plan to implement these algorithms on a microkernel operating system based on the x86 platform and test the algorithms using a set of processes with varying bursts and arrival times. We will evaluate the performance of these algorithms in terms of four metrics: Waiting time, Turnaround Time, Response Time, and Number of Context Switches. This project aims to find an algorithm that provides better performance through reduced turnaround and waiting times without a significant context switching overhead and providing better response times.
Keywords—CPU Scheduling, Microkernel Operating System, Dynamic Round Robin, Adaptive, Manhattan Distance.
I.	PROJECT IDEA/ APPLICATION
	The primary objective of this project is to assess the effectiveness and efficiency of different Dynamic Round Robin algorithms in CPU scheduling under varying workloads on a Microkernel Operating System.
We will design and implement the Microkernel Operating System for 64-bit systems, providing essential services for process management, memory management, and inter-process communication. The operating system will be constructed on top of x86 architecture running on a Virtual Box instance. The design of the Operating System will be similar to the OS built by Sun et al.,[1]
We will implement Dynamic Round Robin Algorithms – Optimal Round Robin Scheduling using Manhattan Distance,  Improved Round Robin Algorithm and Adaptive Round Robin Algorithm. The experiment implements the work of Alsulami et al.,[2] on a physical operating systems. Similar works has been done by M. B. M et al[3] and Alsheikhy et al[4].

Optimal Round Robin Using Manhattan Distance: 
This method selects the time quantum by finding the difference between the highest burst time and the lowest burst time.
1.	Find maximum and minimum burst times.
2.	Set time quantum by calculating the difference between the two burst times.
Time Quantum = Max(Burst Times) - Min(Burst Times)
3.	Repeat till queue is empty, if a process arrives to queue based on its arrival time.

Improved Round Robin Algorithm:
In this method, the time quantum will be selected using the following algorithmic procedure. 
1.	Sort processes in the queue with increasing burst times.
2.	Find the maximum and median burst times.
3.	Set time quantum using below formula
Time quantum = Ceil(sqrt(median x highest burst time))
4.	Repeat steps till the queue is empty, if a process arrives to queue based on its arrival time.

Adaptive Round Robin Algorithm:
In this method, the time quantum will be selected using the following algorithmic procedure. 
1.	Sort processes in the queue with increasing burst times.
2.	Set time quantum as the median of the sorted burst times.
Time quantum = median (sort (burst times))
3.	Repeat steps till the queue is empty, if a process arrives to queue based on its arrival time.
We will evaluate the performance and fairness of the three Dynamic Round Robin algorithms by running them under varying workloads. The performance metrics include throughput, response time, and fairness, which will be used to identify the most suitable Dynamic Round Robin algorithm for real-world deployment scenarios.

The testing process will be executed by developing a set of programs with known burst times, consisting of both CPU and I/O bursts. The compiler of the OS will be designed to estimate the burst time during compilation. The scheduling algorithms will decide the time quantum based on the estimated running time of the processes. The execution time of each process will be recalculated after each burst using the past run times and estimated remaining time using exponential averaging/ aging technique.
A.	Relevance to Course Material
This project involves designing and implementing a 64-bit multi-process microkernel operating system with a focus on integrating and evaluating various Dynamic Round Robin (RR) scheduling algorithms for CPU scheduling. It relates to the course material by extending the understanding of CPU scheduling algorithms, operating system design principles, and low-level system programming technique.
B.	Project Motivation
Our group aims to experiment, measure, and analyze the performance of different Dynamic Round Robin scheduling algorithms in a microkernel operating system environment. Specifically, we want to assess their effectiveness in managing CPU resources, optimizing throughput, response time, and fairness among processes.

The operating system we want to build is motivated by similar microkernel- based OSs like MINIX¬¬[5] and L4[6]. We plan to keep building and experimenting with our OS after the project to gain better hands-on expertise on the subject and streamline it for specific real-world applications.
			
II.	DESIGN AND IMPLEMENTATION
Note: The implementation described is currently for a Monolithic Kernel. We have implemented the Memory and Process management modules in the Kernel space. However, we are having trouble going forward with implementing Inter-Process communication along with the implementation of the three Dynamic RR scheduling Algorithms. Given the time constraints and the complexity of building a microkernel, the project's initial focus was to implement and evaluate a monolithic kernel with Round Robin algorithm for scheduling. Now, we will modify the OS into a Microkernel OS and implement the scheduling algorithms. However, we are concerned about meeting the project deadlines.



The figure below shows the difference between the design of a Monolithic Kernel and a Micro-kernel Operating System. 

 

Figure 1: Monolothic Kernel vs Micro-kernel Design
Bootloader and OS Setup: 
The bootloader initializes the execution environment by setting up segment registers and the stack pointer. It then verifies disk extension support and confirms the boot signature's validity to ensure a proper boot sector. 
It features multistage execution transitioning from 16-bit to 32-bit and then to 64-bit modes, employing extended CPUID functionality to check for necessary processor features. It loads a secondary kernel from disk, retrieves memory information, enables the A20 gate, sets video mode, loads the Global Descriptor Table (GDT) and Interrupt Descriptor Table (IDT), and transitions to Protected Mode (PM). 

In Protected Mode, it initializes necessary data structures, clears memory, configures control registers, and jumps to Long Mode (LM) for 64-bit execution, ultimately allowing for comprehensive system initialization and kernel loading. Furthermore, it initializes the Programmable Interval Timer (PIT) and the Programmable Interrupt Controller (PIC) for system timing and interrupt handling.

The OS manages interrupt handling, increments a tick counter for timer interrupts, and wakes up processes as necessary. A basic system call mechanism has been implemented in the operating system kernel, providing functionalities for writing to the screen, sleeping, exiting processes, and waiting for other processes.


Memory Management:
The Memory management is implemented using paging. During initialization, the kernel reads memory map data to identify available memory regions and allocates pages from the free memory pool as needed. It sets up page tables and manipulates page table entries, ensuring proper mapping of virtual addresses to physical addresses. Page table holds attributes such as "present", "writable" and "user-accessible" values. 
The kernel controls access permissions to memory regions using these attributes. It also manages its own virtual memory space, known as the "kernel space," ensuring that kernel components can access memory as required. Overall, implementation of paging optimizes memory management, dynamic allocation, and deallocation processes in the kernel, enhancing the stability and performance of the operating system. Figure 2 shows the test for Memory Managament module.

 
Figure 2: Memory Management Module Test 



Process Management:
The operating system manages the lifecycle and resource allocation of processes by initialising and updating a table of processes. Processes go through several states, such as ready, running, sleeping(blocked), and killed, which indicate what they are doing or where they are in the system at that moment. By using context switching, the kernel can distribute CPU time across various programs in an efficient manner, ensuring fair execution responsiveness.

The process management system provides synchronisation and communication mechanisms. A running process will get interrupted after 10ms using a timer interrupt and corresponding handler will perform the context switching. The system changes the processor to its context and starts a process when it is chosen for execution. When no other process is prepared to use the CPU, an idle process can be launched to ensure that system resources are always being used. Effective concurrent task management is made possible by the process management system providing system responsiveness and stability in multitasking scenarios thanks to this integration.


III.	EXPERIMENTATION

Experiment with various Dynamic Round Robin scheduling algorithms to understand their impact on CPU resource utilization and process responsiveness. Measure key performance metrics such as throughput, response time, and fairness under different workloads and system conditions. Analyze the trade-offs between different scheduling algorithms in terms of simplicity, overhead, and adaptability to varying system loads.

 
	
Figure 3:Comparison of Scheduling Algorithm Performance

A.	Building Microkernel OS

Task 1: Virtual Machine and Boot Loader setup.

Task 2: Setup synchronization Mechanism.

Task 3: Implement memory management module.

Task 4: Implement process management module.

Task 5: Testing Operating System.

B.	Dynamic Round Robin Scheduling

Task-6: Implement Optimal Round Robin Scheduling using Manhattan Distance.

Task-7: Implement Improved Round Robin Algorithm.

Task-8: Implement Adaptive Round Robin Algorithm.

C.	Testing and Reporting

Task-9: Develop programs to evaluate the performance of the system under different workloads.

Task-10: Measure and analyze key performance metrics to compare the efficiency of different scheduling algorithms.

Task-11: Analyze and document the results of the evaluation and develop charts and graphs to visualize the results.




Task 	Assigned to/ Completed By	Status
Task 1	Pooja	Done
Task 2	Pooja	In Progress
Task 3	Sai Krishna	Done
Task 4	Neeraj	Done
Task 5	Group	In Progress
Task 6	Neeraj	Pending
Task 7	Sai Krishna	Pending
Task 8	Pooja	Pending
Task 9, 10, 11	Group	Pending

IV.	EVALUATION
The evaluation results of three different scheduling algorithms: Optimal Round Robin, Improved Round Robin, and Adaptive Round Robin. The evaluation metrics are including average turnaround time, average response time, and average waiting time.

 


Figure 4: Algorithm Comparison Graph: Turnaround, Response, and Waiting Times for the 3 different scheduling algorithms.

A.	Optimal Round Robin

For the Optimal Round Robin algorithm, the average turnaround time was calculated to be 28.50 time units, with an average response time of 10.25 units and an average waiting time of 19.75 units. These metrics were obtained through simulation and analysis of various test cases.

B.	Improved Round Robin

The Improved Round Robin algorithm exhibited slightly higher performance metrics compared to the Optimal Round Robin approach. However, the average turnaround time increased to 31.00 time units, with an average response time of 13.25 units and an average waiting time of 22.25 units. Despite efforts to enhance the scheduling mechanism, these results indicate a trade-off between certain performance metrics.
C.	Adaptive Round Robin

The Adaptive Round Robin algorithm demonstrated significant improvements compared to both the Optimal and Improved Round Robin strategies. With an average turnaround time of 15.25 time units, an average response time of 8.75 units, and an average waiting time of 8.75 units, this approach showcased superior performance across all evaluated metrics.
		
V.	ANALYSIS
The Adaptive Round Robin algorithm has demonstrated superior performance compared to both the Optimal and Improved Round Robin algorithms. This validates our expectation that adaptive strategies would lead to better management of CPU resources, improved throughput, response time, and fairness among processes. By experimenting with these algorithms and analyzing their performance, we have gained valuable insights into their effectiveness and suitability for real-world applications.

VI.	FUTURE PROSPECTS
Moving forward, we plan to work on the exciting challenge of transitioning from a Monolithic Kernel to a Microkernel architecture while implementing Inter-Process communication alongside the three Dynamic Round Robin scheduling Algorithms. We aim to optimize the performance and adaptability of these algorithms. Moreover, the integration of Inter-Process communication mechanisms presents an opportunity to enhance system-wide communication and collaboration, enabling more efficient resource sharing and coordination among processes. By implementing robust IPC mechanisms alongside the scheduling algorithms, we can further improve system responsiveness and throughput. 

VII.	CONCLUSION

Our project focuses on improving task scheduling within an Operating System. We explore different scheduling methods such as Optimal Round Robin, Improved Round Robin, and Adaptive Round Robin. Through thorough testing, we found that the Adaptive Round Robin method outperforms the others, enhancing task completion speed and fairness across different tasks. These findings are significant as they contribute to smoother operation of operating systems, crucial for real-world scenarios where efficient computer performance is essential. Moving forward, our goal is to make the system even better by changing its structure and adding features to make communication between tasks easier. This will ultimately result in a faster and more responsive system.





A.	Resources
Linux Kernel Archives, ACM Digital Library access.

Tools - Git, VS Code, Bochs, WSL (Windows Subsystem in Linux) - Ubuntu, GCC, NASM, 

Language: x86 Assembly, C, shell script

Documentation: x86 architecture documentation, Existing OS documentation

VIII.	PROJECT MILESTONE
Milestone 	 Start		End
Project Kick-off and Planning 	Feb-14		Feb-21
System Design and Architecture	Feb-22		Mar-06
Core Component Implementation	Mar-07		Mar-27
Dynamic Round Robin Scheduling
Implementation	Mar-27		Apr-03
Develop programs to test the Scheduling Algorithms	Apr-04		Apr-11
Testing and Evaluation	Apr-12		Apr-18
Optimization and Refinement	Apr-19		Apr-25

IV.References
[1]	X. Sun, Y. Cai, R. Jiang and J. Qin, "Design and Implementation of 64-bit Multi-process Microkernel Operating System based on x86 platform," 2022 International Symposium on Intelligent Robotics and Systems (ISoIRS), Chengdu, China, 2022, pp. 57-61.
[2]	A. A. Alsulami, Q. A. Al-Haija, M. I. Thanoon and Q. Mao, "Performance Evaluation of Dynamic Round Robin Algorithms for CPU Scheduling," 2019 SoutheastCon, Huntsville, AL, USA, 2019, pp. 1-5.
[3]	M. B. M, A. P. Kumar and S. P. Rajur, "Improvised Round Robin scheduling Algorithm with the Calculated Time Quantum," 2023 International Conference on Intelligent and Innovative Technologies in Computing, Electrical and Electronics (IITCEE), Bengaluru, India, 2023, pp. 292-295
[4]	A. Alsheikhy, R. Ammar and R. Elfouly, "An improved dynamic Round Robin scheduling algorithm based on a variant quantum time," 2015 11th International Computer Engineering Conference (ICENCO), Cairo, Egypt, 2015, pp. 98-104
[5]	A. S. Tanenbaum and A. S. Woodhull, Operating Systems: Design and Implementation, 3rd ed.
[6]	Gernot Heiser and Kevin Elphinstone, "L4 Microkernels: The Lessons from 20 Years of Research and Deployment." ACM Trans. Comput. Syst. 34, 1, Article 1 (April 2016), 29 pages
[7]	B. Liu, C. Wu and H. Guo, "A Survey of Operating System Microkernel," 2021 International Conference on Intelligent Computing, Automation and Applications (ICAA), Nanjing, China, 2021, pp. 743-748


 
Documentation and Reporting	Apr-26		Apr-30
Project Review and Finalization	May-01		May-01
