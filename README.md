# Dynamic Round Robin Scheduling Algorithms in a Microkernel Operating System

## Abstract

The performance of an operating system (OS) is significantly influenced by its scheduling algorithm. This project aims to evaluate the effectiveness and efficiency of various Dynamic Round Robin algorithms for CPU scheduling on a Microkernel Operating System. We will compare three different Round Robin algorithms: Optimal Round Robin Scheduling using Manhattan Distance, Improved Round Robin Scheduling, and Adaptive Round Robin Algorithm. Our evaluation will focus on key performance metrics such as Waiting Time, Turnaround Time, Response Time, and Number of Context Switches.

## Keywords

- CPU Scheduling
- Microkernel Operating System
- Dynamic Round Robin
- Adaptive
- Manhattan Distance

## Project Idea / Application

The project involves designing and implementing a 64-bit Microkernel Operating System for the x86 architecture. The OS will be built on VirtualBox and will include essential services for process management, memory management, and inter-process communication. We will implement and test three Dynamic Round Robin Scheduling algorithms:

1. **Optimal Round Robin Scheduling using Manhattan Distance**
2. **Improved Round Robin Scheduling**
3. **Adaptive Round Robin Scheduling**

These algorithms will be evaluated under varying workloads to assess their performance in terms of throughput, response time, and fairness.

## Design and Implementation

### Bootloader and OS Setup

- Initializes execution environment and transitions from 16-bit to 64-bit mode.
- Configures memory and system settings for OS loading and initialization.
- Manages interrupt handling and basic system calls.

### Memory Management

- Implemented using paging to allocate and manage virtual memory efficiently.
- Ensures proper mapping of virtual addresses to physical addresses.

### Process Management

- Manages the lifecycle and resource allocation of processes.
- Implements context switching and process scheduling to ensure efficient CPU time distribution.

## Experimentation

We will experiment with the following tasks:

1. **Building Microkernel OS**
   - Setup Virtual Machine and Boot Loader
   - Implement synchronization mechanisms
   - Implement memory and process management modules
   - Test the OS

2. **Dynamic Round Robin Scheduling**
   - Implement Optimal Round Robin Scheduling using Manhattan Distance
   - Implement Improved Round Robin Algorithm
   - Implement Adaptive Round Robin Algorithm

3. **Testing and Reporting**
   - Develop programs to evaluate performance under different workloads
   - Measure and analyze key performance metrics
   - Document and visualize results

## Evaluation

The performance of the scheduling algorithms will be evaluated based on:

- **Optimal Round Robin**: Average turnaround time of 28.50 time units, average response time of 10.25 units, and average waiting time of 19.75 units.
- **Improved Round Robin**: Average turnaround time of 31.00 time units, average response time of 13.25 units, and average waiting time of 22.25 units.
- **Adaptive Round Robin**: Superior performance with an average turnaround time of 15.25 time units, average response time of 8.75 units, and average waiting time of 8.75 units.

## Future Prospects

Future work will focus on transitioning from a Monolithic Kernel to a Microkernel architecture, implementing Inter-Process Communication (IPC), and optimizing the performance of scheduling algorithms. Enhanced IPC mechanisms will aim to improve system responsiveness and resource sharing.

## Conclusion

The project explores various Dynamic Round Robin scheduling algorithms and their impact on OS performance. The Adaptive Round Robin method showed superior performance in terms of task completion speed and fairness. Future work will focus on further refining the system and adding IPC features for improved communication between tasks.

## Resources

- **Documentation**: [x86 architecture documentation](https://example.com/x86-docs), Existing OS documentation
- **Tools**: Git, VS Code, Bochs, WSL (Ubuntu), GCC, NASM
- **Languages**: x86 Assembly, C, Shell Script

## Project Milestones

| Milestone                          | Start   | End     |
|------------------------------------|---------|---------|
| Project Kick-off and Planning      | Feb-14  | Feb-21  |
| System Design and Architecture     | Feb-22  | Mar-06  |
| Core Component Implementation       | Mar-07  | Mar-27  |
| Dynamic Round Robin Scheduling Implementation | Mar-27  | Apr-03  |
| Develop Programs to Test Scheduling Algorithms | Apr-04  | Apr-11  |
| Testing and Evaluation             | Apr-12  | Apr-18  |
| Optimization and Refinement         | Apr-19  | Apr-25  |
| Documentation and Reporting         | Apr-26  | Apr-30  |
| Project Review and Finalization     | May-01  | May-01  |

## References

1. X. Sun, Y. Cai, R. Jiang, and J. Qin, "Design and Implementation of 64-bit Multi-process Microkernel Operating System based on x86 platform," 2022 International Symposium on Intelligent Robotics and Systems (ISoIRS), Chengdu, China, 2022, pp. 57-61.
2. A. A. Alsulami, Q. A. Al-Haija, M. I. Thanoon, and Q. Mao, "Performance Evaluation of Dynamic Round Robin Algorithms for CPU Scheduling," 2019 SoutheastCon, Huntsville, AL, USA, 2019, pp. 1-5.
3. M. B. M, A. P. Kumar, and S. P. Rajur, "Improvised Round Robin Scheduling Algorithm with the Calculated Time Quantum," 2023 International Conference on Intelligent and Innovative Technologies in Computing, Electrical and Electronics (IITCEE), Bengaluru, India, 2023, pp. 292-295.
4. A. Alsheikhy, R. Ammar, and R. Elfouly, "An improved dynamic Round Robin scheduling algorithm based on a variant quantum time," 2015 11th International Computer Engineering Conference (ICENCO), Cairo, Egypt, 2015, pp. 98-104.
5. A. S. Tanenbaum and A. S. Woodhull, Operating Systems: Design and Implementation, 3rd ed.
6. G. Heiser and K. Elphinstone, "L4 Microkernels: The Lessons from 20 Years of Research and Deployment," ACM Trans. Comput. Syst. 34, 1, Article 1 (April 2016), 29 pages.
7. B. Liu, C. Wu, and H. Guo, "A Survey of Operating System Microkernel," 2021 International Conference on Intelligent Computing, Automation and Applications (ICAA), Nanjing, China, 2021, pp. 743-748.

