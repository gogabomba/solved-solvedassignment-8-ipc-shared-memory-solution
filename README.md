Download Link: https://assignmentchef.com/product/solved-solvedassignment-8-ipc-shared-memory-solution
<br>
What is Shared Memory IPC?A shared memory service is an IPC method the OS provides to allocated a segment of memory that can be directly accessed by multiple processes – similar to global data accessible by multiple threads running in a single process. Memory sharing is a simple idea, easy to understand, and favorable to the access speed. The drawbacks are: 1, it is not immune to racing conditions; and 2, it is still restricted within a single host, not over a separate host on a computer network.

As illustrated in example folders, the server (parent) process requests shared memory segments via semget() syscalls in which a key_t key (an integer) and a size (in bytes) are needed. The OS will then allocate the sharable memory and return a memory ID to be used in another syscall shmat() to attach the memory to a local character pointer or be type-cast to other types defined in programs. Subsequent read/write operations are then done via the pointer.

To close (return) the allocated shared-memory segment, the original process that requested it should issue a shmctl() syscall with the memory ID in the arguments.

In this assignment each alphabet process updates its current column position in the shared memory (and sleep for a period), the server process loops to read each position (without sleep). So, updated positions will be read correctly. Therefore, with a semaphore to control the data access between each alphabet and server processes is not needed. (Using semaphores does not change the outcome.) Therefore, only the video semaphore is needed.

Assignment DescriptionIn the assignment folder, the example folders demonstrate syscalls to request segments of shared memory and attach them among processes.

Shared memory segments should be reguested by the server process and given to alphabet processes to use. Each alphabet process can thus know the information it needs. Each alphabet process also updates its current column position into the shared-memory segment for the server to read.

Copy and run the minimum demo. The runtime of your programs must match the demo which is very similar to the previous assignment, except that the server process, after creating all alphabets, should proceed to another loop to read their column positions. And, as each alphabet reaches the finish line, the server displays a placement number at the rightmost column on the row of that alphabet. The top 5 places have an extra 3 asterisk symbols displayed after the number. The server ends this loop when all 26 alphabet processes have reached the finish line.

No message passing is used. Use the shared-memory IPC for all information exchanges, and there is a single semaphore for video display.

See the extra-credit demo. An extra credit (2 points) to incorporate a client.c program that can display/view the progress of the race from a different terminal. The client first draws out the finish-line dots and then loop to access the shared memory to update the display to follow the progress of the race. In order to pass the shared-memory ID, use shell command ./client (shared memory ID) (so the ID will be in the string form of argv[1]).

See the extra-credit-2 demo for a level-2 extra credit (another 2 points), which first lets the client pick a winner via a keypoll process. The picked letter is displayed on the client site (the “GOOD LUCK” message) and passed to the server process via the shared memory. The server will then start the race, and at the end the server returns the result of the points won or lose, and the client site displays that number. The logical rationale of a game play like this is that there can be multiple clients (so each deals its local notifications to display), and the single server does all the point calculations and return them.

The program keypoll.c has its own “include” statements and exits with the ASCII number of the picked alphabet. Only a single occurence of the wait() syscall is allowed in all code, and it is for the client.c to get the picked letter.

The shared memory is used to let each of the 26 alphabet processes access its information: symbol and row number, and semaphore information. The shared memory is also updated by each alphabet process for its current column position after displaying its symbol.

With viewing the race from a separate shell being the client site, the race conducted by the server and its alphabet processes constitute the server site.

Do not use any syscalls for IPC signals, pipes, or message passing. The only “wait-exit” allowed is in the keypoll feature to achieve the level-2 extra credit.

New System CallsYou will need these new ones (see how they are used in given examples):shmget() to request/allocate a sharable memory segment.shmat() to attach a sharable memory segment onto a local char pointer.shmctl() to remove a sharable memory segment.Assignment Turn-inSubmit your source code the same way as required before in previous programming assignments. No E-mail will be accepted, no late turn-ins.

Place to your designated folder only source files: server.c, alphabet.c, common.c, common.h, and Makefile (plus client.c and keypoll.c for extra credits). DO NOT put any other files. If repeated submissions, make a new folder inside this folder and name it V2 (version 2), V3, etc.

Clean up your code with a clean format, preamble header, and comments where suited (and can help the grader to understand your code). Do not mess with your code since it may cause point deduction.