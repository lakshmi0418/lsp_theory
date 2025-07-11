# FILES THEORY

# What are the types of files present in Linux OS?.
Regular files(-):.
These are the most common file type and contain user data, such as text files, images, executables, and scripts. 
Directory Files (d)
Directories are special files that contain references to other files and directories.
Symbolic Links (l)
Symbolic links, or symlinks, are files that point to another file or directory



# How do IPC Objects ,named pipes, be accessed?
named pipes are created using the mkfifo system call 
mkfifo /tmp/myfifo

# User space application sends request to Hardware by using which I/O calls?
    • octl() (Input/Output Control)
    • Used for device-specific input/output operations that cannot be expressed by regular file semantics.
    • read() and write()
    • Standard system calls for reading from and writing to files and devices.
    • mmap() (Memory Mapping)
    • Maps files or devices into memory, allowing applications to access hardware buffers directly.
    • open() and close()

# Why are basic I/O calls called universal I/O calls?
Basic I/O system calls—specifically open(), read(), write(), and close()—are termed "universal I/O calls" because they provide a consistent and uniform interface for performing input and output operations across various types of devices and file systems. This uniformity simplifies application development by abstracting the underlying hardware complexities.

# What is the content of the Inode Object?
    • ile Type and Permissions
    • Indicates the type of file (e.g., regular file, directory, symbolic link) and the access control information (read, write, execute permissions) for the owner, group, and others.
    • Owner Information
    • User ID (UID) of the file's owner.
    • Group ID (GID) of the file's group.
    • Timestamps
    • i_atime: Last access time.
    • i_mtime: Last modification time.
    • i_ctime: Last inode change 
    • File Size
    • The size of the file in bytes.

# In which Object information of the file get stored?

The inode (index node) is a fundamental data structure in Unix-like file systems that stores all metadata about a file or directory, except for its name and actual data

# Kernel uses which object to represent a file?

n the Linux kernel, an open file is represented by the struct file data structure, defined in <linux/fs.h>. This structure is central to the kernel's Virtual File System (VFS) and is created when a process opens a file using system calls like open() or socket(). It is destroyed when the file is closed via close()

# Can we access the file information present in inode from the user application if yes, then
How?

yes, user-space applications can access file information stored in an inode, but they do so indirectly through system calls that retrieve file metadata. Direct access to the inode structure is not permitted in user space due to kernel isolation and security considerations.
# Which system calls are used to access the file information?

    1. stat()
        ◦ Purpose: Retrieves information about a file specified by its path.
        ◦ Usage: int stat(const char *path, struct stat *buf);
        ◦ Description: Populates a struct stat with metadata about the file, such as inode number, file size, permissions, and timestamps.man7.org
    2. fstat()
        ◦ Purpose: Retrieves information about a file specified by its file descriptor.
        ◦ Usage: int fstat(int fd, struct stat *buf);
        ◦ Description: Similar to stat(), but operates on an open file referenced by the file descriptor fd.
    3. lstat()
        ◦ Purpose: Retrieves information about a file specified by its path, without following symbolic links.
        ◦ Usage: int lstat(const char *path, struct stat *buf);
        ◦ Description: If the path refers to a symbolic link, lstat() returns information about the link itself, not the target file.


# ls command internally invoked which system call to access the file information?

    • opendir()
    • Purpose: Opens a directory stream corresponding to the directory name specified by name.
    • Usage in ls: When you run ls on a directory, opendir() is called to open the directory.j
    • readdir()
    • Purpose: Reads the next directory entry from the directory stream referred to by dirp. Each 

# What happens after the kernel finds its inode object?
After the kernel locates an inode object, it proceeds with several steps to facilitate file operations.

# What are the contents of the file object?

    • _dentry: Links the file to its directory entry, which in turn points to the inode. This linkage is crucial for path resolution and namespace management.
    • f_op: Points to a table of function pointers (struct file_operations) that define the file's operations, such as read(), write(), and ioctl(). This allows the kernel to dispatch system calls to the appropriate handler based on the file type.
    • f_pos: Maintains the current position within the file for the next read or write operation. This offset is updated during I/O operations and is specific to each open file descriptor.
    • f_count: Manages the reference count of the file object. Each process that opens the file increments this count, and it is decremented when the file is closed. The file object is freed when the count reaches zero.

# Kernel uses which object to represent the open files?

in the Linux kernel, the object used to represent an open file is the struct file. This structure is created when a file is opened and is destroyed when it is closed

# What is the difference between the primary data and other members of the file object?

Primary Data of struct file
The primary data comprises the essential fields that define the state and behavior of the open file. These 
f_op: Points to the file operations table (struct file_operations), which defines the methods (like read(), write(), ioctl()) that can be performed on the file

secondary Data of struct file
Secondary data consists of additional fields that support the primary data but are not directly involved in the core file operations. These fields may be used for optimization, tracking, or internal management:
    • f_list: Links the file object into various lists (e.g., unused, in-use, or assigned to a superblock).
    • f_reada, f_ramax, f_raend, f_ralen, f_rawin: Read-ahead parameters for optimizing sequential reads.
### Where does the file object base address get stored?

In the Linux kernel, the base address of a struct file object is not explicitly stored in a single, dedicated location.

# When the fd table is created and what is the size of the fd table?
    • Creation: The FD table is created when a new process is initialized.
    • Size: The size of the FD table is determined by the max_fds field in the files_struct structure.

# When is the file object created?

In the Linux kernel, a struct file object is created when a file is opened by a process. 

# What does open() returns?

The open() system call in Linux returns a file descriptor, which is a small, non-negative integer used to reference an open file within a process.

# When a file opens for the first time by using open() calls in your program, what is
returns?

when a file is opened for the first time using the open() system call in a program, it returns a file descriptor, which is a small, non-negative integer. This file descriptor serves as a handle for the open file and is used in subsequent system calls (such as read(), write(), lseek(), fcntl(), etc.) to refer to the open file.

# Why do read() system calls need access to file objects?

ead() Needs the struct file Object
When a user-space application invokes read(), it provides a file descriptor (fd) that indexes into the process's file descriptor table. This table entry points to a struct file object, which contains critical data for the read operation:
    1. File Offset (f_pos): Indicates the current position in the file from which the next read will occur. This offset is updated after each read to ensure sequential access.halolinux.us
    2. File Operations (f_op): Points to a set of function pointers (struct file_operations) that define the operations supported by the file, such as read(), write(), ioctl(), etc. The kernel uses this to invoke the appropriate read() method for the specific file type.
    3. Access Mode (f_mode): Specifies the access permissions for the file (e.g., read, write). The kernel checks this to ensure the operation is permitted.
    4. File Pointer (f_dentry): Links to the dentry structure, which represents the file's name and location in the filesystem hierarchy.
    5. Inode Pointer (f_inode): Points to the inode structure, which contains metadata about the file, such as its size, permissions, and pointers to data blocks.

# Which system call do we use to change the cursor position without reading and
writing on a file?

To change the cursor position (also known as the file offset) in a file without performing any read or write operations, you can use the lseek() system call.

# Can we open the same file from multiple processes? Explain the memory segment in
kernel space?

when multiple processes open the same file, each process receives its own file descriptor. These file descriptors point to the same underlying file object in the kernel, allowing the processes to perform operations like reading or writing to the file. 

kernel Space Memory Segments
Kernel space is reserved for the operating system's kernel, device drivers, and other privileged code. It typically includes the following segments
    • Kernel Code Segment: Contains the executable code of the kernel.
    • Kernel Data Segment: Holds global and static variables used by the kernel.
    • Kernel Stack: Each kernel thread has its own stack, used for function calls and local variables during kernel execution
    • Page Tables: Data structures that map virtual addresses to physical addresses, enabling virtual memory.


# Kernel uses which object to represent a file?

n the Linux kernel, the object used to represent an open file is the struct file, defined in <linux/fs.h>. This structure encapsulates the state and operations associated with an open file for a specific process.

# Is there any limit on no. of files that can be opened from the program?

yes, there is a limit to the number of files a program can open simultaneously in Linux. This limit is controlled by the operating system and can vary based on system configuration and user settings.
# What are the standard I/O calls? Give some examples and what is the alternate name
of standard I/O call?

C programming on Unix-like systems, standard I/O calls refer to system calls that facilitate file operations. These are low-level functions provided by the operating system's kernel, enabling programs to perform tasks such as opening, reading, writing, and closing files.

# Standard I/O System Calls
These system calls are defined in the <fcntl.h> and <unistd.h> headers:
    1. open(): Opens a file and returns a file descriptor.

# What are the basic I/O calls? Give some examples and what is the alternate name of
basic I/O call?
# What is the difference between basic I/O calls and standard I/O calls?

    • asic I/O Calls: Also referred to as low-level I/O, unbuffered I/O, or POSIX I/O.
    • Standard I/O Calls: Sometimes called high-level I/O, buffered I/O, or simply C Standard Library I/O.

# Other than the basic I/O and standard I/O calls,Is there any method to access the file ?

s, in addition to basic I/O and standard I/O calls, there are several other methods to access files,
 each offering distinct advantages depending on the use case.

| Method                      | Use Case                         | Pros                                     | Cons                                      |                                                                                                                                                                               |
| --------------------------- | -------------------------------- | ---------------------------------------- | ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Memory-Mapped Files         | Large file processing            | Efficient, supports random access        | Complex error handling                    |                                                                                                                                                                               |
| Raw Disk Access             | Low-level disk operations        | Direct access                            | Risk of data corruption, OS-specific      |                                                                                                                                                                               |
| Virtual File Systems        | Abstraction over file systems    | Uniform access across systems            | Adds overhead                             |                                                                                                                                                                               |
| Content-Addressable Storage | Data integrity and deduplication | Ensures uniqueness, prevents duplication | Not suitable for frequently changing data |                                                                                                                                                                               |
| File Control Blocks         | Legacy systems                   | Simple file management         
          | 
# How do user space applications get access to the content of inode objects?

User-space applications access the content of inode objects indirectly through the Linux Virtual File System (VFS) layer. The VFS abstracts the underlying filesystem details, providing a uniform interface for user-space applications to interact with files.


# How do you get access to kernel objects/kernel data structure/Information present in
kernel space?

Accessing kernel-space data structures directly from user space is generally prohibited due to strict separation between user and kernel modes in modern operating systems like Linux. This separation ensures system stability, security, and process isolation.
115. Which system calls are used to access the file object?
Open read write lseek close

# Which system calls are used to access the Inode object?

    • pen() / openat(): When an application opens a file, the kernel resolves the file path to a specific inode. This involves:
    • Using the lookup() function to find the inode associated with the file name.
    • Calling iget_locked() to retrieve the inode from the inode cache or load it from disk if it's not already cached.
    • Creating a new struct file object that links to the inode.
    • read() / write(): These system calls perform operations on the file descriptor, which is associated with an inode. The kernel uses the file operations (f_op) defined in the inode's struct inode to handle these operations.
    • stat() / fstat() / lstat(): These system calls retrieve metadata about a file. The kernel accesses the inode to gather information such as file size, permissions, and timestamps.
    • close(): When a file descript
.


