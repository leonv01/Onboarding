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