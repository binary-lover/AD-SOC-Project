---
description: >-
  We will install and configure Active Directory Windows Server and will make
  windows client to join AD
icon: tree
---

# Phase 4 - Setup AD

#### Key ideas & Objectives

* **Network Configuration**: Setting a static IP address for the server and verifying connectivity.
* **AD Installation**: Installing Active Directory Domain Services (AD DS) and promoting the server to a Domain Controller.
* **Domain Creation**: Creating a new forest with the domain name `mujahid.local`.
* **User Management**: Setting up Organizational Units (OUs) for different departments (IT and HR) and creating sample user accounts like Jenny Smith (`jsmith`) and Terry Smith (`tsmith`).
* **Target Machine Integration**: Joining a Windows 10 target machine to the newly created domain by configuring its DNS settings to point to the Domain Controller.
* **Verification**: Logging into the target machine using a domain user account to ensure everything is functional.



#### Network Configuration of Windows Server

1.  Make sure to have this Ip configurations in your Windows AD server

    <figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

#### AD Installation

1. Open Server Manager
   1.  click to manage and > add roles and features<br>

       <figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
   2. Installation type ⇒ role based
   3. Server Selection ⇒ ADDC01&#x20;
   4.  Add this in server roles<br>

       <figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>
   5.  keep clicking on next until you reach to install button and hit install\
       &#x20;

       <figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
   6.  Once you see below message means AD is successfully installed and need to configure<br>

       <figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

#### Domain Creation

1. Promotes the server to domain controller&#x20;
   1.  Click to promote

       <figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>


   2.  creating new forest with the name of `mujahid.local` <br>

       <figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>


   3.  click on next and put the password then next, these are the files that will be created to store data of AD<br>

       <figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>


   4.  When prerequisites are checked click on install, then after installation it will be auto sign out\
       &#x20;

       <figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>


   5.  after restarting it will land to login where you put your AD creds to login<br>

       <figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

#### User Management

1. Create Organisational Unit
   1.

       <figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
   2.

       <figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>


   3.  For best practice we do not create new users in \<users> but use diff method, first we create OU<br>

       <figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>


   4.  I created with name of IT and hit enter, then cllick on IT, right click and <br>

       <figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>


   5. Create 1st user  `jsmith:lucky@786` \
      ![](<../.gitbook/assets/image (20).png>)![](<../.gitbook/assets/image (21).png>)
   6. Create HR OU and create another user terry smith, `tsmith:lucky@786` <br>

#### Target Machine Integration

1. Join Target pc to my domain
   1. spin up target machine
   2.  First need to resolve DNS, go to network adapter \
       its currently have DNS to Google, which be need to set our domain controller 192.168.10.7 and hit enter<br>

       <figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

       <figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

       Now we are good to go to join it to domain server<br>
   3.  Go to About Pc > Advance System Settings <br>

       <figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

       <figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>


   4.  Now need to restart the pc to reflect the changes<br>

       <figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>


   5.  We have sucessfully domain join our target machine<br>

       <figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>



{% hint style="info" %}
<p align="center"><strong>This is if for this phase, now we will move to the next phase</strong> </p>
{% endhint %}
