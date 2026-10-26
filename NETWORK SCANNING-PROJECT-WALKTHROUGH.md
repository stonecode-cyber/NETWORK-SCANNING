### **Network Discovery Detection**

This is my network scanning project where we will bw looking into Internal/External/Vertical/Horizontal scaning. I will be making use of TRYHACKME logs .

**Internal network scan:** Internal network scanning occurs when a system within an organization's network probes other internal assets to identify live hosts, open ports, and running services. it shows that the attacke is still at the DIscovery  Tactics in the MITRE ATT&CK mapping.
**External scan:** ; : External network scanning occurs when a system outside an organization's network probes its public-facing IP addresses to identify active hosts, open ports, and exposed services. it show that we are at the Reiconnaisance staget in MITRE ATT&CK mapping.
**Horizontal Network Scanning:**  Horizontal scanning occurs when a source IP address scans the same port across all  multiple target IP addresses to discover systems running a particular service.
**Vertical network scanning:**: Vertical scanning occurs when a source IP address scans multiple ports on a single target IP address to identify open ports and running services.

**TASK 1: Which file contains logs that showcase internal scanning activity?** 

In this task i will be doing an internal scan to find the file that contain the internal scannimng activities
From the terminal, i navigated to where the file is located using _cd  home/ubuntu//Downloads/logs_ ,  then use the _ls_ command to list all the file  then the  _command head -n2 "log csv file_” for each log file to verify which one has a private IP, with the understading that  that an internal IP of a target is likely to be a private one, and private IPs usually start with a 192.168...... series. as shown in teh screenshot below:

<img width="416" height="271" alt="Image" src="https://github.com/user-attachments/assets/5d5ab2b7-8fd9-4baa-a18b-5d4ab8c333a2" />

As shown above only _**log-session-2.csv**_ has an private IP address o_**f "192.168.230.127",52424,"192.168.230.14**_ which indicate it contain an internal scan.

**TASK 2: How many log entries are present for the internal IP performing internal scanning activity?**

SInce the file with the internal network scan has been identify.The next step is to read the file and pipe it to the cut command with a -_d “,”_ telling the cut command to use the comma as the delimiter (separator between field and column), and the _-f3_ also tells the cut command to extract only the 3rd field (column) from each line. then the pipe to _uniq -c_ is saying remove or detects duplicate lines_**.  cat log-session-2.csv | cut  -d "," -f3 | uniq -c**_
 This only detects duplicates that are consecutive, and -c tells uniq to prefix each unique line with the number of times it occurred.

<img width="407" height="59" alt="Image" src="https://github.com/user-attachments/assets/0ac7051c-f9bd-41ed-8228-0203872dfb17" />

As shown  above, the total number of log in the entries is 2276

**TASK 3: What is the external IP address that is performing external scanning activity?**

In this  task, i went back to the log directory and use the command _**head -n2 log-session-0.csv**_ followed by 2nd and 3rd file to have a look at the IP that perform a scan on the  internal IP  as shown below:
This indicate that the external IP that  scan our internal network is _**203.0.113.25**_

In the next task, i will be dealing with VERTICAL and HORIZONTAL network scaniing
As explained above Horizontal scanning have to do with scanning multiple IP on different port, while Vertical Network scan has to do with network scan of multiple port on the same IP.

**TASK 1: One of the log files contains evidence of a horizontal scan. Which IP range was scanned? Format X.X.X.X/X**

Since we are looking for Scaning wiith multiple IP on the same port,  i make use the _log-session-2.csv_ again as it is the only file that has to do with internal port scan.
 To have a view of all the log files, i send just the 3 to the 6 field to the csv2.txt file using the command  **_cut -d’,’ -f3,4,5,6 log-session-2.csv > csv2.txt_** , I then read the newly created file csv2.txt file using the _**cat**_ command  as shown in the screenshot below:

<img width="427" height="62" alt="Image" src="https://github.com/user-attachments/assets/ec831cac-4241-49b4-9f09-2cec32dced9b" />

<img width="380" height="357" alt="Image" src="https://github.com/user-attachments/assets/6efb1468-7714-4220-8360-a002f84bd395" />
As shown above the muti- IP_address scan  with a singe port number is _203.0.113.0/24_ IP range.

**TASK 2: In the same log file, there is one IP address on which a vertical scan is performed. Which IP address is this?**
As shown in the screenshot of the first task the IP adress that do the port scan of the same IP on different Port is  _192.168.230.145_( VERTICAL NETWROK SCANNING)

**TASK 3: On one of the IP addresses, only a few ports are scanned which host common services. Which are the ports that are scanned on this IP address? Format: port1, port2, port3 in ascending order.**

In this task ,i will use the sme file output of the task above, but diplay the head top 60 using the command below:
 _**cut -d "," -f3,4,5,6 log-session-2.csv |head -n60**_ 
This result to the output shown below:

<img width="449" height="404" alt="Image" src="https://github.com/user-attachments/assets/d424eaaa-4cba-4659-aaca-07a7cdfe7076" />
As shown above, we can see the common port 80(http), 445(server message block SMB), and port 3389(RDP)




