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

We start enumerate users against SMTP service with a simple script by [pentestmonkey - smtp-user-enum](http://pentestmonkey.net/tools/user-enumeration/smtp-user-enum).

![SMTP Enumeration](https://github.com/tesslamx/vulhub-walkthrough/blob/master/HackLAB%20-%20Vulnix/images/smtp%20enumeration.png)

We were able to find some users, the users of our interest could be root and user.

Now, we can go through the Fingerd service found using the following metasploit auxiliary and finger tool: 
  * auxiliary/scanner/finger/finger_users
  * finger [username]@\<host\>

![Finger Enumeration](https://github.com/tesslamx/vulhub-walkthrough/blob/master/HackLAB%20-%20Vulnix/images/finger%20metasploit%20enumeration.png)


#### Step 3. 

Now that we have some valid users for our target, we can make reconnaissance for last port, this one is 111 for the service PortMapper.

We'll try to identify and check for some others RPC services on the target by using the following NMAP script:
* nmap -sV --script=nfs-showmount <target>

![rpcinfo and nfs Enumeration](https://github.com/tesslamx/vulhub-walkthrough/blob/master/HackLAB%20-%20Vulnix/images/rpcinfo%20and%20nfs%20enumeration.png)

It's worthly to note that there are some RPC services available but one important is the NFS service on TCP and UDP, moreover we found a shared ***/home/vulnix***. With it, we might found another user **vulnix** for our user list.


#### Step 4.

If you remember, there is a **SSH** service on our target so then we can try to **brute force** that service with our found users using **Hydra** o **Medusa**.

For our lucky, there was a password for ***user***:***letmein***

![Hydra brute force](https://github.com/tesslamx/vulhub-walkthrough/blob/master/HackLAB%20-%20Vulnix/images/hydra.png)

#### Step 5. 

Then, we try to connect to the target with those credentials by SSH



------
