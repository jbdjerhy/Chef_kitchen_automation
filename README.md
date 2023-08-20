# Chef_kitchen_automation
 
A.	Project Introduction:
 
Satellite Ads Inc is launching their second-generation microsatellites. They need to implement a new cloud-hosted infrastructure to support this second wave of commercial satellites. 
 
 Objectives and scope:
The workload is projected, conservatively, to grow from 2,500 to 141,735 ads per month. The cloud-based infrastructure needs to offer the scalability to adapt to both workload increases and adjustments resulting from various interphase audits and post deployment assessments.  Given the potential for success exceeding the initial projections, the core systems need to spin enough resources to address current demand with a buffer of 10% to avoid usage ever crossing in the red and causing systemwide issues. 
The deployment needs to follow the resource grouping matching the business needs. Templates will be used to automate the creation and deployment of various IT appliances from Satellite Terminal Servers to Scaled Database Servers as indicated in the detailed Project Requirements from the CIO. The design is made of a single core server setup to handle 300 satellites per cluster. Monitoring systems will stay on top of satellite usage and scale out as needed. A queuing service will route helpdesk tickets and will allow log and actively review functionality, load balancing and error handling across the system. 
 
 
 
 
 
 
 
 
 
B.	 Visual Representation:
 
 
 

 
 
 
 
 
 
 
 
 
C.	Automation Script
 
---
#Djerhy Jn Baptiste StudentID: 009923912
#modified .yml script to create the 8 VMs
driver:
  name: vagrant
network:
  - ["public_network"] #additional network interface for VM communication
customize:
  memory: 512 #fixed amount memory for each vm
#Configures the instance provided by the driver. 
provisioner:
  name: chef_zero
  product_name: chef
  product_version: 14.12.9
#program that will run the automated tests. 
verifier:
  name: inspec
#Platfoms section used to indicated which OS will be targeted. 
platforms:
  - name: centos-7 
#Suites section used to edit vm names attribute and reference recipe
suites:
  - name: trial1
    driver:
      vm_hostname: trial1.SparkIT-Games.com
    run_list:
      - recipe[learn_chef_httpd::default]
    attributes:
  - name: trial2
    driver:
      vm_hostname: trial2.SparkIT-Games.com
    run_list:
      - recipe[learn_chef_httpd::default]
    attributes:
  - name: trial3
    driver:
      vm_hostname: trial3.SparkIT-Games.com
    run_list:
      - recipe[learn_chef_httpd::default]
    attributes:
  - name: trial4
    driver:
      vm_hostname: trial4.SparkIT-Games.com
    run_list:
      - recipe[learn_chef_httpd::default]
    attributes:    
  - name: trial5
    driver:
      vm_hostname: trial5.SparkIT-Games.com
    run_list:
      - recipe[learn_chef_httpd::default]
    attributes:
  - name: trial6
    driver:
      vm_hostname: trial6.SparkIT-Games.com
    run_list:
      - recipe[learn_chef_httpd::default]
    attributes:
  - name: trial7
    driver:
      vm_hostname: trial7.SparkIT-Games.com
    run_list:
      - recipe[learn_chef_httpd::default]
    attributes:
  - name: trial8
    driver:
      vm_hostname: trial8.SparkIT-Game.com
    run_list:
      - recipe[learn_chef_httpd::default]
    attributes:
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
A.	Screenshot showing that the automation script executes without errors (from part D):
 
 
 

 
 
 
 

 
 
 
 
 
D.	Diagnostic Report
 
Data Description	Optimal Range	Data and Results	Automation Script Used to Extract Data (text only)	Screenshot of Result of Script
Time to scale from 1 cluster to 200 clusters 
(60,000 advertisements expected at peak global usage) based on 300 satellites per cluster (subject to change based on load testing)
 	15–30 minutes for each cluster	Actual time for 1 cluster: 10m41S
 
 
200 clusters = 36 hours	 
 
 
Kitchen Create	 

 
Time to register a cluster and then quench connections to the load balancer, taking the cluster off-line (start-up, operation, shutdown)
 	1 minute per connection quench, start of cluster launch, and part of time to scale cluster, can be tracked separately as a quench	 	 	 
Peak load averages per system at 200, and 300, satellites per cluster	60% of CPU triggers new cluster launch; if reaching core load at 200 satellites, launch new cluster on 60% CPU loads	Given the current system load for 1 instance: 
 
0.0, 0.1, 0.5
 
 	 
 
 
 
Top	 

 
Write times to the diagnostic data drive
 
 	<30 milliseconds	 
 
 
1073741824 Bytes (1.1 GB) copied, 30.7212 s, 35.0 MB/S	 
 
dd if=/dev/zero of=/root/testfile bs=1G count=1 oflag=direct
 	 

 
Pull time from the game instances (1 Satellite Terminal Server, 1 Web Server, 1 Database, and 1 time server) and initialization time
 	Part of cluster launch 15–30 minutes	 
 
10mn 45s	Kitchen Create
 
Kitchen Converge	 

 
*Average messaging service (queue) time
 
 	<1 minute in queue	 
 
N/A	 
N/A	 
 
N/A
Average latency for the Time server
 
 	<30 milliseconds	Test ping from vm instance to wgu.edu
 
Rtt min/avg/max/mdev = 18.869/27.662/73.201/16.203 ms	 
 
 
 
Ping wgu.ed	 

 
Average latency of each cluster 
 
 	<30 milliseconds	Test ping to localhost
 
Rtt min/avg/max/mdev =0.023/0.184/0.981/0.356 ms	Ping localhost from one of the created instances 	 

 
Network data in and out for each cluster
 
 	<1 second	Test ping to Google.com 
 
Rtt min/avg/max/mdev = 21.770/47.082/73.261/21.737	Ping to google.com from another instance 	 

 
Overall CPU utilization of the environment for each cluster
 	Not >60%	Given the current system load for 1 instance: 
 
0.0, 0.1, 0.5
 	Top 	 

 
*Diagnostic data able to be written by the automation to the correct cloud bucket storage space	Show read/write times <1 second	 
 
 
 
1073741824 bytes (1.1 GB) copied, 6.84678 s, 157 MB/s	Sudo dd if=/dev/zero of=testWriteSpeed.txt bs=1G count=1	 

 
Scaled Satellite Cluster latency
 
 	<30 milliseconds	Test ping to Google.com 
 
Rtt min/avg/max/mdev = 21.770/47.082/73.261/21.737	Ping to google.com from another instance 	 

 
Scaled Satellite Cluster latency between gateway/scaled clusters and core
 
 	<30 milliseconds	Test ping to localhost
 
Rtt min/avg/max/mdev =0.023/0.184/0.981/0.356 ms	Ping localhost from one of the created instances 	 

 
Scaled Satellite Cluster latency between scaled clusters and environment 
 	<30 milliseconds	Test ping to Google.com 
 
Rtt min/avg/max/mdev = 21.770/47.082/73.261/21.737	Ping to google.com from another instance 	 

 
Pull time from the game instances (1 Satellite Terminal Server, 1 Web Server, 1 Database, and 1 time server) and initialization time
 	Part of cluster launch 15–30 minutes	 
 
10mn 45s	Kitchen Create
 
Kitchen Converge	 

 
 
 
 
E.	Web Source:
 
● Getting Started with Test Kitchen – For Test Kitchen setup and initial configuration
- https://learn.chef.io/modules/local-development/ubuntu#/infrastructure-automation
- https://kitchen.ci/docs/getting-started/introduction/ 
 
● Kitchen syntax and tools 
- https://docs.chef.io/config_yml_kitchen.html
 
● Linux Networking commands 
- 7 Linux networking commands that every sysadmin should know | Enable Sysadmin (redhat.com)
 
 
● Kitchen variables information 
- About Provisioners (kitchen.ci)
 
 



