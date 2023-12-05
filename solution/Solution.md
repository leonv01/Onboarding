# Onboarding Solution

# 1. User button LED toggle
<p>
Configure both pins:<br>
<img src="../img/blinki/UserButtonToggle.png" alt="User button configuration"><br>
Set the pin mode of PC13 to <strong>GPIO_Input</strong>
<img src="../img/blinki/UserButtonPinMode.png" alt="User button pin mode"><br>
Add the toggle code to the main loop:<br>
<code>
int main(){<br>
&nbsp;...<br>
&nbsp;while(1){<br>
&ensp;if(!HAL_GPIO_ReadPin(GPIOC, GPIO_PIN_13)){<br>
&nbsp;&nbsp;HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET);<br>
&nbsp;}<br>
&nbsp;else{<br>
&nbsp;&nbsp;HAL GPIO WritePin(GPIOA, GPIO PIN 5 , GPIO PIN RESET);<br>
&nbsp;}<br>
}
</code>

# 2. SSH Key generation and configuration
<p>
To create a new environment variable, go to your Windows search bar and search for <strong>"Edit environment variables for your account"</strong>. <br>
<img src="../img/ssh/EnvironmentVariables.png" alt="Environtment Variable Setup"><br>
Add a new user variable <strong>HOME</strong> and set it to your C-drive home directory, e.g. <strong>C:\Users\user.NAME</strong>.<br>
<img src="../img/ssh/CreateEnvironmentVariable.png" alt="Add Environment Variable"><br>
Generating a new SSH key-pair: <br>
<img src="../img/ssh/GitBashSSH.png" alt="SSH key generation"><br>
To rename it, go into the .ssh directory:
<img src="../img/ssh/SSHRenaming.png" alt="SSH key renaming"><br>
Now copy the public key:
<img src="../img/ssh/SSHPublic.png" alt="SSH public key content"><br>
Adding the key requires you to go to your GitHub account settings &rarr; SSH and GPG keys &rarr; new SSH key:<br>
<img src="../img/ssh/SSHoption.png" alt="GitHub account settings"><br>
Creating the config file:<br>
<img src="../img/ssh/ConfigCreation.png" alt="Config file configuration"><br>
Edit the file with an editor of your choice and add the Host and the path to the corresponding private key: <br>
<img src="../img/ssh/ConfigFileContent.png" alt="Config file content"><br>
Testing the authentification:<br>
<img src="../img/ssh/SSHauthentification.png" alt="SSH authentification"><br>
</p>

# 3. Version Control with Git
<p>
Initializing a local repository:<br>
<img src="../img/git/GitInit.png" alt="Initializing repository"><br>
Creating a remote repository:<br>
<img src="../img/git/GitRemoteRepository.png" alt="Remote repository"><br>
.gitignore file definition:<br>
<img src="../img/git/GitIgnore.png" alt=".gitignore definition"><br>
<img src="../img/git/GitIgnoreContent.png" alt=".gitignore content"><br>
Adding files and committing them with a message:<br>
<img src="../img/git/GitAdd.png" alt="Adding files to the repository"><br>
<img src="../img/git/GitCommit.png" alt="Committing files to the repository"><br>
Creating a new branch:<br>
<img src="../img/git/GitBranch.png" alt="Creating a new branch"><br>
Adding the remote repository with SSH to the local repository:<br>
<img src="../img/git/GitRemoteRepoSSH.png" alt="Adding remote repository"><br>
<img src="../img/git/GitRemoteAdd.png" alt="Adding remote repository to local repository"><br>
Pushing commit to remote repository:<br>
<img src="../img/git/GitPush.png" alt="Pushing to remote repository">
</p>

# 4. Debugger
<p>
After <code>i = 7</code> iterations:<br>
<img src="../img/debugger/debuggerVariables.png" alt="Debugger Variables"><br>
<img src="../img/debugger/DebuggerStep.png" alt="Debugger Step"><br>