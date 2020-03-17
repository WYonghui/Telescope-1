# Telescope

Telescope is a  novel  job scheduling scheme in RDMA-assisted big data processing system. Telescope exploits the structure feature of stage dependency and prioritizes the stages whose completion can enable more schedulable stages. Comprehensive experiments using large-scale traces collected from real world show that Telescope reduces job completion time and job makespan compared to existing schemes.

# Introduction

Since the emergence of big data applications, big data processing systems, such as Hadoop and Spark, have been widely used in both industry and academia. A job in the processing system is commonly represented as a direct acyclic graph (DAG), where a vertex denotes a computation stage
that executes user-defined function and an edge depicts the data transfers between two stages as well as the dependency between them. A stage that reads data from its dependent stages cannot start until all of them are finished. Typically, a computation stage consists of multiple small tasks that execute the same user-defined function. A task is the basic execution unit to perform computation, while multiple tasks can run in parallel to improve resource efficiency. As different jobs with diverse characteristics (e.g., different DAG structures) commonly coexist in the big data processing system, efficient task scheduling is vital for overall system performance.

Traditional scheduling schemes in big data processing systems often give priority to data locality during job scheduling because the network transferring can dominate the job execution time. For a scheduled task, if its input data resides on the same machine with it, we say the task achieves data locality. Otherwise, it needs to read input data across network. Besides, shuffle between stages often involve all to all transfer, where every downstream task needs to read input data from every upstream task. The efficiency of such a communication intensive operation is subject to the network capability. Therefore, existing efficient task scheduling schemes commonly follow the network-optimized design principle. Existing designs optimize data locality during task placement, reduce shuffle traffics by deploying tasks to fewer and closer racks, or balance traffics among cross-rack links.

However, today’s modern datacenters are commonly equipped with high performance networks such as Remote Direct Memory Access (RDMA). With the equipment of RDMA, network is no longer a bottleneck of big data processing systems and the traditional network optimized
scheduling strategies become unsatisfied.

According to our analysis, we verify that the root cause of computing resource under-utilization in RDMA-assisted big data processing system is the lack of schedulable tasks while the system has available slots. Based on the observation, we propose Telescope, a novel job scheduling scheme in RDMA-assisted big data processing system. Telescope investigates stage dependencies, and proposes a stage dependency aware scheduling scheme, which maintains a long-term vision and prioritizes stages whose completion can enable more stages to execute in the subsequent scheduling. We implement Telescope on top of RDMA-Spark, and conduct comprehensive experiments to evaluate its performance using real world cluster traces. Results show that Telescope reduces job completion time and job makespan compared to existing schemes.


ACKNOWLEDGEMENTS   
RDMA-Spark. <http://hibd.cse.ohio-state.edu/#spark>
