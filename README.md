Quick Steps for Impatient Users Like Me
Enable the OpenSSH Authentication Agent service and make it start automatically.
👉 Update 👈
With the latest Windows update Version 10.0.19042.867 I had to re-do this step!
Add your SSH key to the agent with ssh-add on the command line.
Test git integration, if it still asks for your passphrase, continue on.
Add the environment variable $ENV:GIT_SSH=C:\Windows\System32\OpenSSH\ssh.exe to your session, or permanently to your user environment.
Detailed Steps: Overview
Windows has been shipping with OpenSSH for some time now. It includes all the necessary bits for ssh to work alongside Git, but it still seems to need some TLC before it works 100% seamlessly. Here's the steps I've been following with success as of Windows ver 10.0.18362.449 (you can see your Windows 10 version by opening a cmd.exe shell and typing ver).

I assume here that you already have your SSH key setup, and is located at ~/.ssh/id_rsa

Enable the ssh-agent service on your Windows 10 box.
Start-> Type 'Services' and click on the Services App that appears.
Find the OpenSSH Authentication Agent service in the list.
Right-click on the OpenSSH Authentication Agent service, and choose 'Properties'.
Change the Startup type: to Automatic.
Click the Start button to change the service status to Running.
Dismiss the dialog by clicking OK, and close the Services app.
Add your key to the ssh-agent
Open your shell of preference (I'll use Windows Powershell in this example, applies to Powershell Core too).
Add your SSH key to the ssh-agent: ssh-add (you can add the path to your key as the first argument if it differs from the default).
Enter your passphrase if/when prompted to do so.
Try Git + SSH
Open your shell (again, I'm using Powershell) and clone a repo. git clone git@github.com:octocat/Spoon-Knife
If you see this prompt, continue on to the next section:
Enter passphrase for key '/c/Users/your_user_name/.ssh/id_rsa':
Set your GIT_SSH Environment Variable
In any session you can simply set this environment variable and the prompt for your passphrase will stop coming up and ssh will use the ssh-agent on your behalf. Alternatively, you can set your passphrase into your user's environment permanently.

To set GIT_SSH in the current shell only:

Open your shell of preference. (Powershell for me)
Set the environment variable GIT_SSH to the appropriate ssh.exe: $Env:GIT_SSH=$((Get-Command -Name ssh).Source)
Retry the steps in Try Git + SSH above.
To set GIT_SSH permanently

Open File Explorer. Start-> type 'File Explorer' and click on it in the list.
Right-click 'This PC' and click on 'Properties'.
Click on 'Advanced system settings'.
Click the 'Environment Variables...' button.
Under 'User variables for your_user_name' click New...
Set Variable name: field to GIT_SSH
Set the Variable value: field to path-to-ssh.exe (typically C:\Windows\System32\OpenSSH\ssh.exe).
Click OK to dismiss the New User Variable dialog.
Click OK to dismiss the Environment Variables dialog.
Retry the steps in Try Git + SSH above.
