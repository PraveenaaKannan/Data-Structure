This program demonstrates a simplified implementation of a Runtime Process Scheduler using a linked list data structure in the C programming language. It simulates the Round Robin scheduling algorithm, which is commonly used in operating systems to manage the execution of multiple processes. Each process is represented as a node in a linked list, containing a unique process ID and burst time. The scheduler cycles through the processes, allocating a fixed time quantum for each process's execution. If a process's burst time exceeds the time quantum, it is preempted and placed back in the queue to wait for its next turn. The program also includes functionality to handle user input for the number of processes, their burst times, and the time quantum, as well as memory management to ensure efficient resource utilization. Through real-time output, the program provides insights into the execution order and time allocation of processes, making it a useful educational tool for understanding basic process scheduling concepts.                                                                                                                                                                                 This program demonstrates a simplified implementation of a Runtime Process Scheduler using a linked list data structure in the C programming language. It simulates the Round Robin scheduling algorithm, which is commonly used in operating systems to manage the execution of multiple processes. Each process is represented as a node in a linked list, containing a unique process ID and burst time. The scheduler cycles through the processes, allocating a fixed time quantum for each process's execution. If a process's burst time exceeds the time quantum, it is preempted and placed back in the queue to wait for its next turn. The program also includes functionality to handle user input for the number of processes, their burst times, and the time quantum, as well as memory management to ensure efficient resource utilization. Through real-time output, the program provides insights into the execution order and time allocation of processes, making it a useful educational tool for understanding basic process scheduling concepts.                                                                                                               #include <stdio.h>
#include <stdlib.h>
struct process {
    int pid;
    int burstTime;
    struct process* next;
};
struct process* front = NULL;
void addProcess(int burstTime) {
    static int pidCounter = 1;
    struct process* newProcess = (struct process*)malloc(sizeof(struct process));
    if (newProcess == NULL) {
        printf("Memory allocation failed\n");
        exit(EXIT_FAILURE);
    }
    newProcess->pid = pidCounter++;
    newProcess->burstTime = burstTime;
    newProcess->next = NULL;
    if (front == NULL) {
        front = newProcess;
    } else {
        struct process* temp = front;
        while (temp->next != NULL) {
            temp = temp->next;
        }
        temp->next = newProcess;
    }
}
void roundRobin(int quantum) {
    int totalBurstTime = 0;
    struct process* temp = front;
    while (temp != NULL) {
        totalBurstTime += temp->burstTime;
        temp = temp->next;
    }
    while (totalBurstTime > 0) {
        temp = front;
        while (temp != NULL) {
            if (temp->burstTime > 0) {
                if (temp->burstTime > quantum) {
                    printf("Process %d executes for %d units\n", temp->pid, quantum);
                    totalBurstTime -= quantum;
                    temp->burstTime -= quantum;
                } else {
                    printf("Process %d executes for %d units\n", temp->pid, temp->burstTime);
                    totalBurstTime -= temp->burstTime;
                    temp->burstTime = 0;
                }
            }
            temp = temp->next;
        }
    }
}
void freeProcesses() {
    struct process* temp;
    while (front != NULL) {
        temp = front;
        front = front->next;
        free(temp);
    }
}
void inputProcesses() {
    int numProcesses, burstTime, quantum;
    printf("Enter the number of processes: ");
    scanf("%d", &numProcesses);
    for (int i = 0; i < numProcesses; i++) {
        printf("Enter burst time for process %d: ", i + 1);
        scanf("%d", &burstTime);
        addProcess(burstTime);
    }
    printf("Enter the time quantum: ");
    scanf("%d", &quantum);
}
int main() {
    inputProcesses();
    printf("\nMethod selected: Round Robin Scheduling\n");
    int quantum;
    printf("Enter the time quantum: ");
    scanf("%d", &quantum);
    roundRobin(quantum)
   freeProcesses();
    return 0;
}
                                                                                                                                                                                                                          
