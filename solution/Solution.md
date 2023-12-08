# Onboarding Solution

## 1. User button LED toggle
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

### 1.2 SSH Key generation and configuration
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

### 1.3 Version Control with Git
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

### 1.4 Debugger
<p>
After <code>i = 7</code> iterations:<br>
<img src="../img/debugger/debuggerVariables.png" alt="Debugger Variables"><br>
<img src="../img/debugger/DebuggerStep.png" alt="Debugger Step"><br>

--

## 2. Toolchain
### 2.1 Setting up workspace
<p>
Installing WSL:<br>
<code>wsl --install</code>
</p>
List all distributions:<br>
<code>wsl --list --online</code>
</p>
<p>
Update/Upgrade apt and install make package:<br>
<ol>
<li><code>sudo apt -y update</code></li>
<li><code>sudo apt -y upgrade</code></li>
<li><code>sudo apt -y install make</code></li>
<li><code>sudo apt -y install libncurses-dev</code></li>
</ol>
</p>
<p>
Adding compiler etc. to the linux system:<br>
<ol>
<li><code>sudo tar xjf gcc-arm-none-eabi-*.bz2 -C /usr/share/</code></li>
<li><code>sudo ln -s /usr/share/gcc-arm-eabi-YOUR VERSION/bin/arm-none-eabi-gcc /usr/bin/arm-none-eabi-gcc</code></li>
<li><code>sudo ln -s /usr/share/gcc-arm-eabi-YOUR VERSION/bin/arm-none-eabi-gdb /usr/bin/arm-none-eabi-gdb</code></li>
<li><code>sudo ln -s /usr/share/gcc-arm-eabi-YOUR VERSION/bin/arm-none-eabi-g++ /usr/bin/arm-none-eabi-g++</code></li>
<li><code>sudo ln -s /usr/share/gcc-arm-eabi-YOUR VERSION/bin/arm-none-eabi-size /usr/bin/arm-none-eabi-size</code></li>
<li><code>sudo ln -s /usr/share/gcc-arm-eabi-YOUR VERSION/bin/arm-none-eabi-objcopy /usr/bin/arm-none-eabi-objcopy</code></li>
</ol>
</p>
<p>
Making libncurses compatible with arm-none-eabi-gdb:<br>
<ul>
<li> <code>sudo ln -s /usr/lib/x86 64-linux-gnu/libncurses.so.6 /usr/lib/x86 64-linux-gnu/libncurses.so.5</code>
<li> <code>sudo ln -s /usr/lib/x86 64-linux-gnu/libncurses.so.6 /usr/lib/x86 64-linux-gnu/libtinfo.so.5</code>
</ul>
</p>

### 2.2 ST-Link
<p>
Makefile advancement:<br>
<code>flash: all</code><br>
<code>ST-LINK_CLI.exe -P $(TARGET).bin 0x08000000 -V -Rst</code>
</p>
<p>
<code>clean</code><br>
<code>ST-LINK_CLI.exe -ME</code>
</p>

--

## 3 CAN bus
### 3.1 Setting up a new project
<p>
Project ioc file:<br>
<img src="../img/can/canIoc.png" alt="Project ioc file">
</p>
CAN configuration:<br>
<img src="../img/can/canConfig.png" alt="Project ioc file">
</p>

### 3.3 Sending Messages
Setting up CAN bus:<br>
<code>
CAN_TxHeaderTypeDef TxHeader;<br>
uint8_t TxData[8];<br>
uint32_t TxMailbox;<br>
<br>
int main(void){<br>
&nbsp;...<br>
&nbsp;char message[] = {'H', 'e', 'l', 'l', 'o'};<br>
&nbsp;HAL_CAN_Start(&hcan1);<br>
&nbsp;if (HAL_CAN_ActivateNotification(&hcan1, CAN_IT_RX_FIFO0_MSG_PENDING) != HAL_OK)<br>
&nbsp;{<br>
&nbsp;&nbsp;Error_Handler();<br>
&nbsp;}<br>
}<br>
TxHeader.IDE = CAN_ID_STD;<br>
TxHeader.StdId = 0x446;<br>
TxHeader.DLC = sizeof(message);<br>
TxHeader.RTR = CAN_RTR_DATA;<br>
<br>
while(1){<br>
&nbsp;if(!HAL_GPIO_ReadPin(GPIOC, GPIO_PIN_13)){<br>
&nbsp;&nbsp;TxHeader.IDE = CAN_ID_STD;<br>
&nbsp;&nbsp;TxHeader.StdId = 0x446;<br>
&nbsp;&nbsp;TxHeader.DLC = sizeof(message);<br>
&nbsp;&nbsp;TxHeader.RTR = CAN_RTR_DATA;<br>
<br>
&nbsp;&nbsp;for(int i = 0; i < sizeof(message); i++){<br>
&nbsp;&nbsp;&nbsp;TxData[i] = message[i];<br>
&nbsp;&nbsp;}<br>
&nbsp;&nbsp;HAL_CAN_AddTxMessage(&hcan1, &TxHeader, TxData, &TxMailbox);<br>
&nbsp;&nbsp;HAL_Delay(100);<br>
&nbsp;}<br>
}
</code>

### 3.4 Receiving Messages
<code>
CAN_RxHeaderTypeDef RxHeader;<br>
uint8_t RxData[8];<br>

int datacheck;<br>
void HAL_CAN_RxFifo0MsgPendingCallback(CAN_HandleTypeDef *hcan){<br>
&nbsp;if(HAL_CAN_GetRxMessage(hcan, CAN_RX_FIFO0, &RxHeader, RxData) != HAL_OK){<br>
&nbsp;&nbsp;Error_Handler();<br>
&nbsp;}<br>
<br>
&nbsp;if(RxHeader.DLC == 2){<br>
&nbsp;&nbsp;datacheck = 1;<br>
&nbsp;}<br>
}<br>
<br>
int main(void){<br>
&nbsp;...<br>
&nbsp;char answer[] = {'D', 'o', 'n', 'e'};<br>
&nbsp;...<br>
<br>
&nbsp;while(1){<br>
&nbsp;&nbsp;if(datacheck){<br>
&nbsp;&nbsp;int delay = RxData[1];<br>
&nbsp;&nbsp;for(int i = 0; i < RxData[0]; i++){<br>
&nbsp;&nbsp;&nbsp;HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET);<br>
&nbsp;&nbsp;&nbsp;HAL_Delay(delay);<br>
&nbsp;&nbsp;&nbsp;HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_RESET);<br>
&nbsp;&nbsp;&nbsp;HAL_Delay(delay);<br>
&nbsp;&nbsp;}<br>
<br>
&nbsp;&nbsp;TxHeader.IDE = CAN_ID_STD;<br>
&nbsp;&nbsp;TxHeader.StdId = 0x123;<br>
&nbsp;&nbsp;TxHeader.DLC = sizeof(answer);<br>
&nbsp;&nbsp;TxHeader.RTR = CAN_RTR_DATA;<br>
<br>
&nbsp;&nbsp;for(int i = 0; i < sizeof(answer); i++){<br>
&nbsp;&nbsp;&nbsp;TxData[i] = answer[i];<br>
&nbsp;&nbsp;}<br>
&nbsp;&nbsp;HAL_CAN_AddTxMessage(&hcan1, &TxHeader, TxData, &TxMailbox);<br>
&nbsp;&nbsp;datacheck = 0;<br>
&nbsp;}<br>
}
<br>
...
<br>
static void MX_CAN1_Init(void){<br>
&nbsp;hcan1.Instance = CAN1;<br>
&nbsp;hcan1.Init.Prescaler = 12;<br>
&nbsp;hcan1.Init.Mode = CAN_MODE_NORMAL;<br>
&nbsp;hcan1.Init.SyncJumpWidth = CAN_SJW_1TQ;<br>
&nbsp;hcan1.Init.TimeSeg1 = CAN_BS1_11TQ;<br>
&nbsp;hcan1.Init.TimeSeg2 = CAN_BS2_2TQ;<br>
&nbsp;hcan1.Init.TimeTriggeredMode = DISABLE;<br>
&nbsp;hcan1.Init.AutoBusOff = DISABLE;<br>
&nbsp;hcan1.Init.AutoWakeUp = DISABLE;<br>
&nbsp;hcan1.Init.AutoRetransmission = DISABLE;<br>
&nbsp;hcan1.Init.ReceiveFifoLocked = DISABLE;<br>
&nbsp;hcan1.Init.TransmitFifoPriority = DISABLE;<br>
&nbsp;if (HAL_CAN_Init(&hcan1) != HAL_OK)<br>
&nbsp;{<br>
&nbsp;&nbsp;Error_Handler();<br>
&nbsp;}<br>
<br>
&nbsp;CAN_FilterTypeDef canFilterConfig;<br>
<br>
&nbsp;canFilterConfig.FilterActivation = CAN_FILTER_ENABLE;<br>
&nbsp;canFilterConfig.FilterBank = 10;<br>
&nbsp;canFilterConfig.FilterFIFOAssignment = CAN_RX_FIFO0;<br>
&nbsp;canFilterConfig.FilterIdHigh = 0x1F << 5;<br>
&nbsp;canFilterConfig.FilterIdLow = 0x0000;<br>
&nbsp;canFilterConfig.FilterMaskIdHigh = 0x4F0 << 5;<br>
&nbsp;canFilterConfig.FilterMaskIdLow = 0x0000;<br>
&nbsp;canFilterConfig.FilterMode = CAN_FILTERMODE_IDMASK;<br>
&nbsp;canFilterConfig.FilterScale = CAN_FILTERSCALE_32BIT;<br>
&nbsp;canFilterConfig.SlaveStartFilterBank = 0;<br>
<br>
&nbsp;HAL_CAN_ConfigFilter(&hcan1, &canFilterConfig);<br>
}
</code>


### 3.5 Filter Messages
<code>
&nbsp;CAN_FilterTypeDef canFilterConfig;<br>
<br>
&nbsp;canFilterConfig.FilterActivation = CAN_FILTER_ENABLE;<br>
&nbsp;canFilterConfig.FilterBank = 10;<br>
&nbsp;canFilterConfig.FilterFIFOAssignment = CAN_RX_FIFO0;<br>
&nbsp;canFilterConfig.FilterIdHigh = 0x1F << 5;<br>
&nbsp;canFilterConfig.FilterIdLow = 0x0000;<br>
&nbsp;canFilterConfig.FilterMaskIdHigh = 0x4F0 << 5;<br>
&nbsp;canFilterConfig.FilterMaskIdLow = 0x0000;<br>
&nbsp;canFilterConfig.FilterMode = CAN_FILTERMODE_IDMASK;<br>
&nbsp;canFilterConfig.FilterScale = CAN_FILTERSCALE_32BIT;<br>
&nbsp;canFilterConfig.SlaveStartFilterBank = 0;<br>
<br>
&nbsp;HAL_CAN_ConfigFilter(&hcan1, &canFilterConfig);<br>
}
</code>