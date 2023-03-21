# Page_Turner

## Description 
For this project we were assigned to solve any problem with a robotic arm. We decided to solve the problem of turning the pages of a book. Whenever your hands are full or tired, the robot will turn the page with the press of a button! The robot can turn your pages both forward and backward to make sure that book is read exactly how you want. 

## Plan
[Link to Planning Document](https://docs.google.com/document/d/1uazbonK2YwQbwLo_14c-oHcuRzRMN066gJCfVLczz6s/edit?usp=sharing)

## List of Materials 
- Acrylic sheets 
- 3D Printed Parts 
- Metro Express Board
- Servos (both mirco and standard) 
- Wires 
- Grippy Wheel  
- Buttons
- Switch
- Led 
- Screws/Nuts
- 6 volt batteries (and case) 
- Binder Clips (optional) 

## Wiring 
![Screenshot (19)](https://user-images.githubusercontent.com/71406903/226720688-e2d9b6da-e5a8-4aaf-bd68-35bd76b62acd.png)

## Code 
```import time
import board
import pwmio
from adafruit_motor import servo
from digitalio import DigitalInOut, Direction, Pull

btn1 = DigitalInOut(board.D11)
btn1.direction = Direction.INPUT
btn1.pull = Pull.DOWN

btn2 = DigitalInOut(board.D12)
btn2.direction = Direction.INPUT
btn2.pull = Pull.DOWN

switch = DigitalInOut(board.D13)
switch.direction = Direction.INPUT
switch.pull = Pull.DOWN

# create a PWMOut object on Pin A2.
pwm1 = pwmio.PWMOut(board.D10, duty_cycle=2 ** 15, frequency=50)
pwm2 = pwmio.PWMOut(board.D9, duty_cycle=2 ** 15, frequency=50)
pwm3 = pwmio.PWMOut(board.D8, duty_cycle=2 ** 15, frequency=50)

# Create a servo object, my_servo.

large_servo = servo.Servo(pwm1)
small_servo = servo.Servo(pwm2)
arm_servo = servo.Servo(pwm3)
#arm_servo = servo.Servo(pwm3, min_pulse=600, max_pulse=2700)

#set servoes to starting position
    #arm servo to UP
arm_servo.angle = 90


    #lg servo to STOP
    #sm servo to .... right? 180?


while True:
    if switch.value:
        print ("pageturneron")
        led.value = True
        time.sleep(0.5)
    large_servo.angle = 90
    time.sleep(0.5)
        #this is just the UP example. copy and flip values for DOWN
    # If button is pressed
    if btn1.value:
        print ("btn1 pressed")

        # is the sm servo in the correct position?
        # Drop lg servo
        #We will write code for "arm servo" to move lg servo, here.
        # Rotate Lg servo for # seconds
        for a in range(90, 110, +1):
            arm_servo.angle = a
            time.sleep(0.1)

        #armAng = 0
        #armAng = 0
        time.sleep(1)
        large_servo.angle = 0
        time.sleep(0.8)
        print("largego")
        large_servo.angle = 90
        print("largestop")
        #wait 0.x seconds to allow page to "Settle"
        time.sleep(1)
        # move Sm servo
        small_servo.angle = 180
        print("smallgo")
        time.sleep(2)
        time.sleep(2)
        small_servo.angle = 0
        print("smallDone")
        time.sleep(1)
        # Lift Lg servo and Sm servo

    elif btn2.value:
        print ("btn2 pressed")
        for a in range(90, 60, -1):
            arm_servo.angle = a
            time.sleep(0.1)
        small_servo.angle = 180
        time.sleep(1)
        large_servo.angle = 180
        time.sleep(0.8)
        print("largego")
        large_servo.angle = 90

        print("largestop")
        time.sleep(1)
    #wait 0.x seconds to allow page to "Settle"
        time.sleep(1)
    # move Sm servo
        small_servo.angle = 180
        print("smallgo")
        time.sleep(2)
        small_servo.angle = 0
        print("smallDone")
        time.sleep(1)
    # Lift Lg servo and Sm
```

## Design 
[Link to OnShape Design](https://cvilleschools.onshape.com/documents/01a062a01cddf5eb5958f3b2/w/d8f47f2354e056dddd10364c/e/1d6924a5a86b305411a16dc0?renderMode=0&uiState=641a05a887911329f0cfaed9)

For our design we used 4 sheets of acrylic to creat a sloped box which can hold a box of the top. We used 3 different servos; a standard servo which would change the position of the wheel depending on whihc was you wanted to turn the book, a continuous standard servo which had a wheel attached to turn up the page, and a micro servo which was a little arm to flip the page at the end. 

## Pictures
![IMG-1387](https://user-images.githubusercontent.com/71406903/226722292-77394f71-088f-4ee6-abc7-5b80fffda8a7.jpg)
![IMG-1388](https://user-images.githubusercontent.com/71406903/226722373-69d73415-9304-455d-a0ea-791310243df5.jpg)
![IMG-1389](https://user-images.githubusercontent.com/71406903/226722420-f2df5f98-77da-423e-8e64-28e486d03b7f.jpg)


## Problems/Limitations 
During this project we ran into a few problems but nothing too major. For the code there was a problem with VScode on the computer so we had to switch to MU which wasn't bad because they both use CircuitPython. Also with the code in the end we realized that the servo that positioned the wheel was going to far and it would have to be different for each book size. We addressed the problem so it wouldn't turn to far, however we didn't fully get to make the robot work for alkl different sizes of books, but if we had more time we would've used a potentiometer to change the positioning of the wheel to its desired location. On the CAD side of things after we printed we realized that in OnShape the acrylic was angled at a cartain degree and the laser cutter isn't able to cut the edge like that so we had to sand it down to get it to our desired angle. We also realized that we had used box joints instead of laser joints so our friction-fit pieces were lose. To fix that it wasn't too hard we just increased the width of the pieces by 0.16mm so when we reprinted the pieces fit in perfectly. The only limitations we had was a limited amount of time to finish the project, winter break, and a limited amount of materials. Overall none of these problems were a huge deal in our project just minor issues that we had to address. 

## Reflection
Overall this project was pretty fun, we got to explore how to do many new things healping stengthen our knowledge in both CAD and code. This year we switched to CircuitPython so this project yhelped us get better at how to code using VScode and MU. For CAD we learnt that when connecting laser cut parts at an angle you need to cut the edges shorter so they will not over lap. We worked very well together trhoughout this projetc splitting it up equally as we both worked to create a working arm. We were able to create a robot to move the pages of a book, however we ran out of time to make the robot work for all different kinds of books, but we know what we would do if we ever had to do this project again. If we did this project again we would probably change the design of the "box" and add a potentiometer to get the positioning of the wheel right for all different kinds of books. This project was very fun and we learned many new skills along the way.
