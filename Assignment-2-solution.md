# Assignment 2 - Top 8 IP Address Counter

## 🧩 Objective

The goal of this assignment is to identify the **top 8 IP addresses** that hit a web server the most, based on the provided `logfile`.

we are required to write a script (with **no file extension**) that:

* Reads from an existing `logfile`
* Counts the number of hits per IP address
* Displays the **top 8 most frequent IP addresses** in descending order of hits
* Outputs results in this format:

  ```
  <ip_address> <number_of_hits>
  ```

---

## 🧠 Understanding the Problem

Every line in the web server log file starts with the **IP address** of the client that made the request.
We simply need to count how many times each unique IP appears and display the 8 highest counts.

---

## ⚙️ Script Implementation

Below is the Bash script (`count`) that fulfills the requirements:

 * Step 1: Extract only the first field (IP address) from each log line
 * Step 2: Sort the IPs alphabetically (required before counting)
 * Step 3: Use uniq -c to count occurrences of each unique IP
 * Step 4: Sort numerically and in reverse order (most hits first)
 * Step 5: Display only the top 8 results
 * Step 6: Swap the order so output is in format: <ip_address> <number_of_hits>


```bash
#!/bin/bash

# Define the path to the log file (must be in same directory as this script)
logfile="logfile"

cat "$logfile" | awk '{print $1}' | sort | \
uniq -c | sort -nr | head -8 | \
awk '{print $2, $1}'


# Example Output:
# 92.6.41.236 22
# 186.248.72.9 19
# 81.243.137.36 18
# 217.118.78.16 15
# 213.118.39.51 15
# 93.146.139.64 14
# 80.116.15.0 14
# 186.213.159.176 11

```


## ▶️ How to Run

1. Make the script executable:

   ```bash
   chmod +x count
   ```
2. Ensure the `logfile` is in the same directory.
3. Run the script:

   ```bash
   ./count
   ```


✅ Ready to run using `./count`
