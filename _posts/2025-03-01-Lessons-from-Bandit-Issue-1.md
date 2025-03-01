# Issue 1

## Introduction

Cybersecurity isn’t something you learn just by reading—you have to get your hands dirty. OverTheWire’s *Bandit* wargame is an excellent introduction to Linux and security fundamentals, providing real-world challenges that help you develop essential skills. This series will break down key concepts, useful commands, and practical problem-solving techniques.

I’ve been daily driving Linux Mint (shoutout to Xia’s release!) for about six months now, and while I’ve enjoyed the experience, many tasks can still be done using the GUI thanks to Cinnamon. That means I don’t always have to rely on the terminal—but I want to. Maybe one day I’ll be running Arch with Wayland like the pros, but for now, I want to make sure my command-line skills are solid before making that leap.

## Why *Bandit*?

*Bandit* is a challenge designed to teach Linux through hands-on problem-solving. By connecting to a remote server via SSH, you work through levels that teach essential skills like file management, permissions, and uncovering hidden data. These challenges are invaluable for anyone interested in cybersecurity, ethical hacking, or system administration.

## What to Expect

This series has three main goals:

- Explain the logic behind each challenge to deepen understanding.
- Showcase my knowledge and progress in cybersecurity fundamentals.
- Encourage discussion and knowledge-sharing to make learning easier.

*Bandit* is a structured and fun way to sharpen Linux skills. I’ve completed levels 0-2 so far, so let’s go over what I’ve learned.

---

## Key Takeaways from Levels 0-2

### The Role of SSH in Cybersecurity

SSH (Secure Shell) is an essential tool for securely accessing remote systems. It encrypts communication between devices, making it a critical part of system administration and cybersecurity. The `ssh` command allows remote access, and understanding different options—like `-p` to specify a port (`ssh -p 2220 user@host`) or `-v` for verbose output (`ssh -v user@host`)—helps with troubleshooting and security.

### Mastering Linux Navigation

Knowing how to move around the Linux filesystem is key to efficiency. Basic commands like `ls` (list files), `cd` (change directories), and `cat` (view file contents) help users explore and manage systems effectively. Becoming comfortable with these commands builds confidence and speeds up workflow in the terminal.

### Understanding File Structures and Security

File organization is just as important as navigation. The `du` (disk usage) command helps locate large files and directories, which can uncover unexpected storage use or hidden files. Meanwhile, the `file` command identifies a file’s actual type, which is useful for detecting misnamed executables or disguised malware. Knowing how to analyze files in this way is a crucial skill for cybersecurity.

### Developing a Hacker’s Mindset

Hacking isn’t just about executing commands—it’s about thinking critically, adapting to challenges, and uncovering hidden details. *Bandit* doesn’t just teach Linux skills; it helps develop a problem-solving mentality. Every challenge requires analyzing the situation, experimenting with different approaches, and thinking creatively. By working through these levels, you’re not just learning the command line—you’re learning how to approach problems like a security professional.

---

## Encouraging Hands-on Practice and Further Learning

One of the best ways to reinforce what you’ve learned is through active practice. Even though Mint’s GUI makes things easy, I push myself to use the terminal whenever possible. Running commands, tweaking system configurations, and troubleshooting issues directly in the shell has helped me build confidence and deepen my understanding of Linux.

The Linux `man` (manual) pages are an invaluable resource for learning commands in-depth. Instead of memorizing syntax, I rely on documentation (`man ssh`, `man ls`, etc.), which makes it easier to adapt to new tools and problem-solving scenarios.

I also plan to explore more advanced wargames beyond *Bandit*. Future series will cover challenges like *Narnia* and *Leviathan*, which introduce deeper topics such as binary exploitation and privilege escalation. As I progress through them, I’ll document my experiences just as I am with *Bandit*, providing insights and lessons along the way.

---

This journey is just beginning, and I’m excited to continue learning. Stay tuned!
