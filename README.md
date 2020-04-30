#4180_Final_Project

Idea: The Robot is simulating an automation robot at a shipping facility or factory.

## Getting Started



### The code requirements are:

* The Robot should follow a predetermined path.
* We should be able to scan QR codes and determine a path.
* The Robot should avoid obstacles.
* Perform cool audio and lights. 

### Parts used:


1. Raspberry pi 3
2. Sonar
3. Pi camera
4. Google cloud
5. RGB LED
6. H-bridge
7. Power Pack
8. 2x DC motors

#### 



## Deployment Demo Link

[Demo Link click here ](https://youtu.be/LeDUM39YSuk)

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

The sonar and h-bridge was the most diffult to calibrate with limited resources.

```
#Libraries
import RPi.GPIO as GPIO
import time
 
#GPIO Mode (BOARD / BCM)
GPIO.setmode(GPIO.BCM)
 
#set GPIO Pins
GPIO_TRIGGER = 18
GPIO_ECHO = 24
 
#set GPIO direction (IN / OUT)
GPIO.setup(GPIO_TRIGGER, GPIO.OUT)
GPIO.setup(GPIO_ECHO, GPIO.IN)
 
def distance():
    # set Trigger to HIGH
    GPIO.output(GPIO_TRIGGER, True)
 
    # set Trigger after 0.01ms to LOW
    time.sleep(0.00001)
    GPIO.output(GPIO_TRIGGER, False)
 
    StartTime = time.time()
    StopTime = time.time()
 
    # save StartTime
    while GPIO.input(GPIO_ECHO) == 0:
        StartTime = time.time()
 
    # save time of arrival
    while GPIO.input(GPIO_ECHO) == 1:
        StopTime = time.time()
 
    # time difference between start and arrival
    TimeElapsed = StopTime - StartTime
    # multiply with the sonic speed (34300 cm/s)
    # and divide by 2, because there and back
    distance = (TimeElapsed * 34300) / 2
 
    return distance
 
if __name__ == '__main__':
    try:
        while True:
            dist = distance()
            print ("Measured Distance = %.1f cm" % dist)
            time.sleep(1)
 
        # Reset by pressing CTRL + C
    except KeyboardInterrupt:
        print("Measurement stopped by User")
        GPIO.cleanup()
```


## Built With

* [OpenCV](opencv.org) - Used to decode QR codes
* [Zbar](https://pypi.org/project/zbar/) - Barcode scanning
* [ROME](https://www.raspberrypi.org/) - Used as our micro controller

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.



## Authors

* **Jose Sanchez**
* **Keith Jones**


## License

*

## Acknowledgments

* https://www.youtube.com/watch?v=L90WS-ptnvI
* [DC motors](https://www.instructables.com/id/Raspberry-PI-L298N-Dual-H-Bridge-DC-Motor/) - H-bridge setup

