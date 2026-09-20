Project Iceberg N GUI beta — An Introduction
What it is
Project Iceberg is a 32-bit operating system for x86 computers, built entirely from scratch. It boots from a CD image, brings up its own graphical desktop, and gives the user windows, a file explorer, a text editor and a command terminal.

It is roughly 50 KB of compiled code, written in C and x86 assembly.

An independent kernel
Iceberg does not use the Linux kernel. It is also not built on Windows NT, any BSD, or any other existing operating system. Every line that runs after the firmware hands over control — the bootloader, the interrupt handling, the drivers, the graphics, the filesystem, the desktop — was written for this project.

This matters because most software that calls itself an "OS" is in fact a distribution: a familiar kernel with a different set of programs arranged on top of it. Ubuntu, Fedora and Android all share the Linux kernel. Iceberg shares its kernel with nothing. The only outside code it relies on is the machine's own BIOS, which it asks for disk reads and a graphics mode during the first moments of boot, and a font that was converted into a bitmap before the system was compiled.

How it starts
When the computer powers on, the firmware reads the first sector of the CD and runs it. That sector is Iceberg's bootloader. In real mode it reads the rest of itself from disk, measures how much memory the machine has, asks the BIOS for a linear-framebuffer video mode — 1024x768 in 32-bit colour if the hardware offers it, with several fallbacks if not — enables the A20 line, installs a flat descriptor table, and switches the processor into 32-bit protected mode. It then jumps into the kernel.

From that point the BIOS is gone and the kernel is alone with the hardware.

What the kernel does
It installs an interrupt table and remaps the interrupt controller, starts a 100 Hz timer, and talks directly to the PS/2 controller to read the keyboard and the mouse, including the scroll wheel. It reads the clock from CMOS. It manages memory with a simple allocator. Everything drawn on screen is composed in an off-screen buffer and copied to the framebuffer a rectangle at a time, so the desktop stays smooth without a graphics driver of any kind.

Files live in a small in-memory filesystem called Floe. It has directories, creation, deletion and editing, and it arrives preloaded with a sample tree. Because it is held in RAM, its contents are gone when the machine restarts.

What the user sees
A desktop with a wallpaper, icons and a taskbar. Windows can be dragged, minimised and closed, and they stack in a proper order. The file explorer switches between icon and list views and can browse, create, rename and delete. The text editor saves back to the RAM disk. The terminal accepts about fifteen commands. Four themes are included, and the start menu can restart or shut down the machine.

What it is for
Iceberg is a teaching system, not a working one. It has no processes, no protected memory, no networking, no permanent storage and no system-call interface — the foundations a production operating system is built on. What it does offer is a complete, readable path from the first instruction the firmware executes to a mouse cursor moving on screen, small enough that one person can hold all of it in their head.

That is the point of it.
