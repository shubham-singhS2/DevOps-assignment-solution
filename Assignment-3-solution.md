# Assignment 3 - Troubleshooting High Load Average on Linux

## 🧠 Summary
In this assignment, the system reported a **high load average** (e.g., `44.28, 33.34, 30.44`), indicating too many processes waiting for CPU or I/O resources.  
The goal is to systematically identify the root cause — whether it’s **CPU overload, disk I/O bottleneck, memory exhaustion, or a faulty process** — using standard Linux troubleshooting tools.

---

## 1. Check Overall System Load
```bash
uptime
top    # or htop
```
**Look for:**  
- High **%us** or **%sy** → CPU-bound load  
- High **%wa** → I/O wait  

---

## 2. Identify Top Resource Consumers
```bash
ps -eo pid,ppid,cmd,%cpu,%mem,stat --sort=-%cpu | head
```
Check if the process is necessary — if not, **kill** or **restart** it to reduce system load.

---

## 3. Check Disk I/O
```bash
iostat -xz 1 3
iotop
```
**Look for:**  
- **%util** near 100% → disk saturation  
- **await** > 10 ms → slow disk response  

---

## 4. Check Memory and Swap
```bash
free -m
vmstat 1 5
```
**Look for:**  
- Low available memory  
- High swap activity (**si**, **so** > 0)  

---

## 5. Review Logs
```bash
journalctl -xe | tail -20
```
**Look for:**  
- Disk errors  
- OOM (Out of Memory) killer events  
- Kernel warnings  

---

✅ **Conclusion:**  
By checking CPU, disk I/O, memory, and system logs, we can quickly determine whether the high load average is caused by resource contention, a stuck process, or system misconfiguration — and take corrective action such as stopping runaway processes, freeing memory, or investigating I/O bottlenecks.
