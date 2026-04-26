# Results

This assignment adds symlink support to xv6. The kernel now defines a new symbolic-link inode type, exposes a `symlink()` system call to user space, and teaches `sys_open()` to follow symlink chains when opening a file.

The implementation stores the symlink target path inside the symlink inode itself. When a symlink is opened, xv6 reads the stored target and resolves it recursively, with a fixed maximum depth to avoid infinite loops in cyclic links.

The user-side interface was updated as well: the new syscall is wired through the syscall table and user stubs, and `testsymlink` was added to verify creation, resolution, and cyclic-link handling.

Overall, the change enables basic symbolic links in xv6 while keeping the implementation simple and bounded by fixed path and recursion limits.