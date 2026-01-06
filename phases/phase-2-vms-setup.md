---
description: Virtual Machines Installation Phase
icon: computer-classic
---

# Phase 2 - VMs Setup

### **1. The Virtual Machine Lineup**&#x20;

By the end of this installation phase, you will have:

* Target Machine: Windows 10 Pro.
* Attacker Machine: Kali Linux.
* Active Directory Server: Windows Server 2022.
* SIEM Server: Ubuntu Server 22.04 (to run Splunk).

#### 1.1 Install Windows 10 pro

{% hint style="success" %}
Downloaded Windows 10 ISO from: [Click here to Download](https://www.microsoft.com/en-us/software-download/windows10ISO)
{% endhint %}

I set up with these Configuration

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

#### 1.2 Install Attacker machine

{% hint style="success" %}
Download Kali Virtualbox file from: [Click Here to Download](https://www.kali.org/get-kali/#kali-virtual-machines)
{% endhint %}

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Extract the file and double click on _<mark style="color:blue;">**kali-linux-2025.4-virtualbox-amd64.vbox**</mark>_ with Blue icon.<br>

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

It will install and sutup automatically all the things&#x20;

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Default Password

User: kali\
Pass: kali
{% endhint %}

#### 1.3 Install Windows Server 2022

{% hint style="success" %}
Download windows server 2020 ISO from:   [Click here to Download](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)
{% endhint %}

{% hint style="info" %}
I have Downloaded Windows Server 2020 64 bit edition  English (United States)
{% endhint %}

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

**For Installation**

1. used 4 GB ram and 50 GB hard disk space
2.  Select 2nd option for Desktop navigation else you will end up with a CLI, and it will be difficult to navigate.

    <figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>


3.  Now we will have this screen after installation:<br>

    <figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

    \
    Setup your password accordingly make sure its very secure and confidential.\
    my case: `lucky@786`
4. Once the Screen presents then you must input `CRTL + ALT + DEL` \
   for this go to input > keyboard > Insert CRTL-Alt-Del&#x20;
5.  Login with your password, it will open auto open SERVER MANAGER Application<br>

    <figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>



{% hint style="info" %}
We will install and configure the Active Directory in Phase 4
{% endhint %}

#### 1.4 Install Ubuntu Server

{% hint style="success" %}
Download Ubuntu Server 24.04.3 LTS from:   [Click here to Download](https://ubuntu.com/download/server/thank-you?version=24.04.3\&architecture=amd64\&lts=true)
{% endhint %}

Since This server will run Splunk and lots of data be ingested we need more ram so i am moving with below details and Hard disk space for 100 GB.

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

1. Start the machine and select Try and install Ubuntu server
2.  Keep all settings by default and hit to Done, Done Done Done until you see below screen, where you put your details and passwords my pass: `lucky@786`<br>

    <figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>
3.  Hit done after filling inputs it will start installing, hit enter to reboot now<br>

    <figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>


4.  If failed unmounting /cdrom comes just hit enter <br>

    <figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>
5.  now hit enter once again to begin with login use credential to login into server

    <figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>
6. Once login just run `sudo apt-get sudo update && apt-get upgrade -y` for update the system

{% hint style="info" %}
<p align="center"><strong>This is if for this phase, now we will move to the next phase</strong> </p>
{% endhint %}
