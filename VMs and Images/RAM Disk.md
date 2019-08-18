# RAM Disk


In-memory disk. **Data is held in memory**, but it is structured to look like a HDD.

- Allocate high performance memory to use as a disk
- A RAM disk has **very low latency and high performance**
- Used when an application expects a file system structure and can store data in memory. This way RAM can behave like the file system.
- No storage redundancy or flexibility.
- **Shares memory with applications**, only provision RAM disk if you have surplus memory on a VM.
- Content stays only as long as the VM is up