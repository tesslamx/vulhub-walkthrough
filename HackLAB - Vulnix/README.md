# HackLAB - Vulnix



It is just a personal walkthrough about this lab to make it easier for those who are new on the infosec world.

For more information about Vulnix Lab [here](https://www.vulnhub.com/entry/hacklab-vulnix,48/).

------

#### Step 1.

Find the IP for the lab, one way could be by using the tool ***netdiscover***.

![Netdiscover output](https://github.com/tesslamx/vulhub-walkthrough/blob/master/HackLAB%20-%20Vulnix/images/netdiscover.png)

On my case wasa the IP: ***192.168.6.155***


#### Step 2. 

No we have the IP of the lab, we launch a NMAP scanning to check for ports and services on the target:

![NMAP output](https://github.com/tesslamx/vulhub-walkthrough/blob/master/HackLAB%20-%20Vulnix/images/nmap.png)

Some interesting ports at this moment would be the following: 

| Port  | Service |
| ------------- | ------------- |
| 25  | SMTP  |
| 79  | Fingerd  |
| 79  | Port-Mapper  |


These ones would be good for us to start a enumeration phase and check if we can find some valid users on the target.

------
