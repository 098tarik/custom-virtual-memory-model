# Virtual Memory Simulator

A virtual memory management simulation implemented in C. This project demonstrates paging, page faults, and page replacement algorithms.

## Requirements
**This project requires a Linux environment to compile and run.**
It relies on POSIX-specific headers and features (`sys/mman.h`, `ucontext.h`, signals) to simulate hardware page faults.
- **Linux** (Ubuntu, Fedora, etc.)
- **WSL** (Windows Subsystem for Linux) on Windows
- **macOS** (may require slight adjustments for `ucontext` definitions)

**Note:** This project will *not* compile with MinGW or Visual Studio on Windows directly.

## Overview
This program simulates a virtual memory system mapping virtual pages to physical frames using a page table. It handles page faults by swapping pages in from an emulated disk.

It supports multiple page replacement policies:
- **FIFO**: First-In, First-Out.
- **RAND**: Random page replacement.
- **CUSTOM**: A custom prefetching algorithm that attempts to load the next sequential page.

## Building the Project
To compile the project, run:
```bash
make
```
This generates the `virtmem` executable.

## Running the Simulation

Usage:
```bash
./virtmem <npages> <nframes> <policy> <program>
```

- `<npages>`: Number of pages in the virtual address space.
- `<nframes>`: Number of physical frames available.
- `<policy>`: Replacement policy (`fifo`, `rand`, or `custom`).
- `<program>`: The test program to run (`alpha`, `beta`, `gamma`, `delta`).

### Arguments Detail
- **npages**: Must be >= 1.
- **nframes**: Must be >= 1.
- **policy**: 
  - `fifo`: Evicts the oldest page.
  - `rand`: Evicts a random page.
  - `custom`: Uses a predictive prefetching strategy.
- **program**:
  - `alpha`: Linear scan access pattern.
  - `beta`: Random access pattern.
  - `gamma` / `delta`: Other specific access patterns to test algorithm performance.

## Examples

Run with 100 pages, 10 frames, FIFO policy, executing the 'scan' program (alpha):
```bash
./virtmem 100 10 fifo alpha
```

Run with 50 pages, 5 frames, Random policy, executing the 'sort' program (beta):
```bash
./virtmem 50 5 rand beta
```

## Output
The program will simulate memory accesses and output the final statistics:
- **Page Faults**: Number of times a page had to be fetched from disk.
- **Disk Reads**: Number of blocks read from the swap disk.
- **Disk Writes**: Number of blocks written to the swap disk (evicted dirty pages).

```plaintext
Summary: Page Faults - 120 | Disk Reads - 120 | Disk Writes - 45
```
# custom-virtual-memory-model
# custom-virtual-memory-model
