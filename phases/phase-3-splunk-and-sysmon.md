---
description: We will be installing and configuring Splunk and Sysmon in our VMs
icon: book
---

# Phase  3 - Splunk & Sysmon

In this phase of this Active Directory Project series, the primary objective is to bridge the gap between attacking a system and detecting that activity using professional tools.

#### Key Ideas & Objectives

* **Executing a Brute Force Attack**: You will use Kali Linux and a tool called Crowbar to perform a Brute Force attack against a user via the Remote Desktop Protocol (RDP) .
* **Analyzing Telemetry in Splunk**: After the attack, you will use Splunk to query and identify the specific "Event IDs" (like 4625 for failed logons and 4624 for successful logons) that indicate an attack has occurred.
* **Testing with Atomic Red Team**: You will install and run Atomic Red Team on the target machine. This framework maps to the MITRE ATT\&CK matrix, allowing you to generate "malicious" telemetry (like creating local accounts or script execution) to see if your current security setup can actually detect it.

For working all the vms in the same network we will create a network that will have same subnet and all have internet access. To do so here is the following steps.

#### Installing Splunk and configure&#x20;

&#x20;Got to networks > Create Network > Assign and name IPs and keep DHCP enabled > Hit Apply

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

For Each Machine now need to connect to the same network that we created like this:

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>



1. We will set the splunk with static ip
2.  To do that, make the following changes in the file<br>

    <div align="left"><figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure></div>
3.  now type

    ```
    sudo netplan apply
    ```

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

4. Now go to splunk website to download the file _**4.x+, or 5.4.x kernel Linux distributions**_\
   _**.deb**_

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

5.  To transfer this file to Ubuntu server we will install virtual-box guest addition on ubuntu.<br>

    ```
    sudo apt-get install virtualbox-guest-additions-iso -y
    ```

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

6.  Now do the following steps to mount the folder where you have downloaded the splunk file, and reboot the Ubuntu server<br>

    ```
    sudo reboot
    ```

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

7.  Now we will add new user in Ubuntu Server in `vboxsf`  group, we need to install additional utils that is&#x20;

    ```
    sudo apt-get install virtualbox-guest-utils
    sudo reboot 
    ```

**Adding user**&#x20;

```
sudo adduser mujahid vboxsf
```

**Create new direcotry share and mount shared folder directory to /**&#x73;hare

```
sudo mount -t vboxsf -o uid=1000,gid=1000 Downloads /share
```

{% hint style="info" %}
if you can't access the files in share folder then just exit the session and re login
{% endhint %}

now we have splunk ready to install in /share folder

<div align="left"><figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure></div>

Install Splunk now with follwoing cmd&#x20;

```
sudo dpkg -i <splunk.file.deb>
```

now when it finished head over to /opt/splunk folder\
and switch to splunk user

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

8. **Start Splunk**:\
   as a splunk user below is cmd to start splunk
   1. ```
      cd bin
      ./splunk start
      ```
   2. Now we will set this auto start whenever the machine boots splunk start automatically.
   3. ```
      sudo ./splunk enable boot-start -user splunk    
      ```
   4.

       <figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>
9. Install splunk Universal Forwarder and Sysmon on target machine and server
   1.  First Need to rename the target PC -> Target-PC and reboot<br>

       <div align="left"><figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure></div>
   2.  Change the IP address of target machine to 192.168.10.100<br>

       <figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

       <div align="left"><figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure></div>
   3. Now installing Universal Forwarder on target PC
      1.  go to [Download](https://www.splunk.com/en_us/download/universal-forwarder/thank-you-universalforwarder.html) and download the Universal Forwarder for windows 10.<br>

          <figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>
      2. double click > \
         ![](<../.gitbook/assets/image (57).png>)![](<../.gitbook/assets/image (58).png>)![](<../.gitbook/assets/image (59).png>) and hit next and install&#x20;
   4. Download sysmon now
      1. click [here](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon) tod ownload sysmon
      2. download **sysmon olaf** config click [here](https://raw.githubusercontent.com/olafhartong/sysmon-modular/refs/heads/master/sysmonconfig.xml)
      3.  extract sysmon zip and open power shell with administrator permission on sysmon folder<br>

          <figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>


   5. Instruct our splunk folder to what we want to send over the the splunk server
      1. for that lets configure input.conf in c>program files>splunkuniversalfolder> etc> system> local,
      2. we will create new input.conf so that default input.conf will not get effected
      3.  below is the code that you should paste in local dir as inputs.conf&#x20;

          ```
          [WinEventLog://Application]
          index = endpoint
          disabled = false

          [WinEventLog://Security]
          index = endpoint
          disabled = false

          [WinEventLog://System]
          index = endpoint
          disabled = false

          [WinEventLog://Microsoft-Windows-Sysmon/Operational]
          index = endpoint
          disabled = false
          renderXml = true
          source = XmlWinEventLog:Microsoft-Windows-Sysmon/Operational
          ```
      4. whenever we change input.conf need to restart splunk Universal Forwarder
         1.  run service as administrator and search for S`plunkFolder` service<br>

             <figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

             hit apply and click ok.&#x20;
   6.  Head over to splunk login page give it the username and pass and we have some final configurations to do.<br>

       <figure><img src="../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>
   7. we will create new index called `endpoint` as our inputs.conf specify&#x20;
      1.  got to indexes \
          ![](<../.gitbook/assets/image (63).png>)

          <figure><img src="../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>
      2. now enable splunk to receive data \
         ![](<../.gitbook/assets/image (65).png>)![](<../.gitbook/assets/image (66).png>)![](<../.gitbook/assets/image (67).png>)
   8.  Head over to:<br>

       <figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>
   9.  in search bar search `index="endpoint"` and you will start recieving logs from windows target machine<br>

       <figure><img src="../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

       If you are not getting any logs must re check all process again and restart the `SplunkFolder` service and try to see the logs again

{% hint style="info" %}
Do same thing for the AD server (install sysmon and splunk folder and configure it)
{% endhint %}

After setting up we can see both hosts are now available<br>

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
<p align="center"><strong>This is if for this phase, now we will move to the next phase</strong> </p>
{% endhint %}
