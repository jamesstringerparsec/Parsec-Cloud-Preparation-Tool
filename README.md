                           ((//////                                
                         #######//////                             
                         ##########(/////.                         
                         #############(/////,                      
                         #################/////*                   
                         #######/############////.                 
                         #######/// ##########////                 
                         #######///    /#######///                 
                         #######///     #######///                 
                         #######///     #######///                 
                         #######////    #######///                 
                         ########////// #######///                 
                         ###########////#######///                 
                           ####################///                 
                               ################///                 
                                 *#############///                 
                                     ##########///                 
                                        ######(*                   
                                                           
                           
                                       
                    ~Parsec Self Hosted Cloud Setup Script~

### We're hiring:
We're hiring an experienced solutions architect on the US East Coast: [See here](https://careers.parsec.app/o/sales-engineer-solutions-architect)

### Parsec Cloud Preparation Tool
This script sets up your cloud computer with a bunch of settings and drivers
to make your life easier.  
                    
It's provided with no warranty, so use it at your own risk.

### Who this script is for:
Home users who want to experiment with creating their own cloud server to play games.  

If you are an IT person or business owner who is looking to roll out Parsec enabled cloud desktops for your business, you must license a [Parsec Teams subscription](https://parsec.app/teams/).

### Instructions:                    
1. Set up your GPU accelerated cloud machine on Microsoft Azure, Amazon AWS, Google Cloud or Paperspace.  
2. Azure, AWS, Google: Log in via RDP and make note of the password - you'll need it later - Paperspace: Connect via Paperspace web app.
3. Open Powershell on the cloud machine.
4. Copy the below code and follow the instructions in the script - you'll see them in RED

### Special notes for Google Cloud users:
Do not select "Turn on Display Device" when setting up the instance, this will cause you to have a display that cannot be removed. Parsec can't use this display and you will need to start again from scratch if you create an instance with that option enabled.

### Copy this code into Powershell (you may need to press enter at the end):
```
[Net.ServicePointManager]::SecurityProtocol = "tls12, tls11, tls" 
$ScriptWebArchive = "https://github.com/parsec-cloud/Parsec-Cloud-Preparation-Tool/archive/master.zip"  
$LocalArchivePath = "$ENV:UserProfile\Downloads\Parsec-Cloud-Preparation-Tool"  
(New-Object System.Net.WebClient).DownloadFile($ScriptWebArchive, "$LocalArchivePath.zip")  
Expand-Archive "$LocalArchivePath.zip" -DestinationPath $LocalArchivePath -Force  
CD $LocalArchivePath\Parsec-Cloud-Preparation-Tool-master\ | powershell.exe .\Loader.ps1  
```

This tool supports:

### OS:
Server 2016  
Server 2019
                    
### CLOUD SKU:
AWS G3.4xLarge    (Tesla M60)  
AWS G2.2xLarge    (GRID K520)  
AWS G4dn.xLarge   (Tesla T4 with vGaming driver)  
Azure NV6         (Tesla M60)  
Paperspace P4000  (Quadro P4000)  
Paperspace P5000  (Quadro P5000)  
Google P100 VW    (Tesla P100 with Virtual Workstation Driver)  
Google P4 VW      (Tesla P4 with Virtual Workstation Driver)  
Google T4 VW      (Tesla T4 with Virtual Workstation Driver)  

### RDP:  
Only use RDP to intially setup the instance. Parsec and RDP are not friendly with each other.  

### Issues:
Q. Stuck at 24%  
A. Keep waiting, this installation takes a while.

Q. My cloud machine is stuck at 1366x768  
A. Make sure you use GPU Update Tool to install the driver, and on Google Cloud you need to select the Virtual Workstation option when selecting an NVIDIA GPU when setting up an instance.

Q. My Xbox 360 Controller isn't detected in Windows Server 2019  
A. You will need to visit Device Manager, and choose to Automatically Update "Virtual Xbox 360 Controller" listed under the Unknown Devices catagory in Device Manager.

Q. I made a mistake when adding my AWS access key or I want to remove it on my G4DN Instance  
A. Open Powershell and type `Remove-AWSCredentialProfile -ProfileName GPUUpdateG4Dn` - This will remove the profile from the machine.

Q. What about GPU X or Cloud Server Y - when will they be supported?  
A. That's on you to test the script and describe the errors you see, do not create an issue in Github that does not contain an issue.  Do not create an issue without any actual diagnosis information or error messages.  

Q. How do I change my wallpaper?  
A. Delete the Wallpaper registry value from HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\System  
  
Q. I created an Amazon AMI using this script but when I create a machine from the AMI I can't select high display resolutions above 1366x768  
A. AWS adds some persistent routes to machines which will need to be deleted if you want the NVIDIA Driver to be licensed and display all features and resolutions.  You can do this via  `route print` then making note of the persistant routes and using `route -p DELETE NETWORK.ADDRESS.OF.ROUTE`.  After a reboot the machine should allow high resolutions.  

Q. I connect to my cloud machine with Parsec and see a Parsec logo on the desktop, and the Windows Task bar, but when I click icons in the task bar, nothing happens.  
A. There is another screen on the cloud machine that Parsec can't capture, that is set to your default/primary display. Do the following to switch the primary display to the screen that Parsec can capture.  

1. Connect to the host via Parssec
2. Press CTRL + Shift + i (this will enter into immersive mode)
3. Press Windows Key + P
4. Press Down Arrow, Down Arrow, Enter.

