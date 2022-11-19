#  Traffic Light Manipulation

### Creating a traffic light signal using 3 LED's and 1 push button to turn on and off the LEDs. Also implement Hardware Debounce circuitry for the push button.
### Note: you should change values in registers DDRx PINx PORTx for GPIO, and should not use pinMode(), digitalRead()/Write() functions in your code You can use tinkercad or wokwi.com as simulation platform 
***
## Simulation Diagram
![Simulation Diagram](https://raw.githubusercontent.com/NIKHIL-RAJIV/Bi0s-Tasks/main/Traffic%20Light%20Signal/Simulation%20Diagram.png)
***

## **CODE**
```c++
void setup() {
  DDRB = B000111;  
  PORTD = B00000100;
}
int x=1;
void loop() {
  if(PIND & B00000100){
    PORTB &= B000000;
  }
  if(!(PIND & B00000100)){
    if (x==1){
      PORTB |= B000100;
      delay(1000);
      x++;
    }
    else if (x==2){
      PORTB |= B000010;
      delay(1000);
      x++;
    }
    else if (x==3){
      PORTB |= B000001;
      delay(1000);
      x=x-2;
    }
  PORTB &= B000000; 
  }
}    
```
***
 <a href = "https://www.tinkercad.com/things/1aVAjg8JF9S?sharecode=HvIojrx8ZKMSaHNUnXjFEnkdb0EYVQDNVz71-tgkapE"> <img src ="https://img.shields.io/badge/Thinkercad%20File-Click%20Here%20to%20Simulate-brightgreen" width = 320 align = center> </a>
***

