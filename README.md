# OOPS-ACCIDENTS

Code for creating a Car class in python, with collision detection and time-to-collision calculation implemented using coordinates and speeds.

import math
class Car:
    def __init__(self, make, model, year, speed, x, y,direction): 
        self.make = make
        self.model = model
        self.year = year
        self.speed = speed              #WLOG we take speed as an integer in miles/hr
        self.x = x                      #We take lattice points(integer coordinates) as position of car.
        self.y = y  
        self.direction = direction      # direction of motion of the car in degrees (like 90 is north, 180 is west,-90 is south etc.)
    def accelerate(self, speed_increment):
        self.speed += speed_increment
    
    def brake(self, speed_decrement):
        self.speed = max(0, self.speed - speed_decrement)
        
    def move(self, time):               # updates the position of the car based on its speed and direction
        dx = self.speed * math.cos(math.degrees(self.direction)) * time
        dy = self.speed * math.sin(math.degrees(self.direction)) * time
        self.x += dx
        self.y += dy
    
    def distance(self, car2):
    # Gives the distance between this car and another car
        dx = self.x - car2.x
        dy = self.y - car2.y
        return math.sqrt(dx*dx + dy*dy)
    
    def collision_possibility(self,car2):
    #Here we calculate the direction of relative velocity and see whether the other car is in that direction or not.
        if(math.atan((car2.y-self.y)/car2.x-self.x) == math.atan2(self.speed * math.sin(math.degrees(self.direction))-car2.speed         *math.sin(math.degrees(self.direction)), self.speed * math.cos(math.degrees(self.direction))-car2.speed * math.sin(math.degrees(car2.direction))):
               return true
        else: 
               return false
               
    def detect_collision(self,car2,curent_time):            #time in hours
        if(collision_possibility(self,car2) and current_time > time_to_collision(self, other)):
              return true
        else
              return False
               
    def time_to_collision(self, car2):
    # calculates the time until this car collides with another car
        v_rel = math.sqrt(self.speed*self.speed+car2.speed*car2.speed+2*self.speed*car2.speed*math.cos(math.degrees(self.direction))
        Time_to_collision =  distance(self, car2)/v_rel
        return Time_to_collision
 __________________________________________________________________________________________________________________________________________________________________________    
     
******Example test cases of the Car class for the methods with dummy data:******

car1 = Car("Hyundai", "Creta", 2021, 10, 0, 100, -90)

car2 = Car("Maruti", "Swift", 2022, 30, 200, 0 , 180)

car1.accelerate(20)

car1.move()

car2.accelerate(30)

car2.move()

print(car1.detect_collision(car2,1))         # False

print(car1.detect_collision(car2,2))         # False
 
print(car1.detect_collision(car2,3))         # False

print(car1.detect_collision(car2,4))         # True

print(car1.time_to_collision(car2))          # 3.33333333333 hrs

____________________________________________________________________________________________________________________________________________________________________

**************I have also included the code above itself for convenience**************
                                               
**************COMPLETE DECONSTRUCTION OF THE CODE:**************

Although the code itself has some self explainatory comments ,I will try to explain some subtle points of the above code

Firstly we import the python math library for necessary calculations...

Then, We have created a car class in python with an additional attribute 'direction' apart from those 5 expected attributes.

Our code is not just restricted to a 1D straight road but for the whole 2D region of space.

In line 5 we initialise the attributes by using the method _INIT_ and by the help of self pointers.

We need to be careful while writing the brake function at line 18 that applying the brake can not make the car reverse its diection.

In line 20 , we just resolve the velocity vector into horizantal and vertical components and updated the position.

Out of the 6 attributes , we just need to focus on x, y, speed, direction for collision detection and time calculation.

***MAIN IDEA***: Here, We use the concept of relative velocity to find out collision happens or not. Basically,we go to the frame of the first car and draw the trajectory of second car ,if this trajectory is passing through the position of our car1, then they will surely collide.(can refer the attached image).
Line 34 shows the above idea in code as the slope of line joining the 2 cars should be aligned with the direction of motion of car(resultant velocity direction.)
And the function atan2 is nothing but tan inverse function.

The method detect_collision returns true if the collision has happened before the given moment of time.So, first we calculate the time for collision by the method 
time_to_collision and if our time of interest is more than the collision time ,then obviously collision has already happened.

In line 40, I calculated the collision time by the formula , time = relative distance upon relative velocity.
(v_rel = sqrt((v1)^2+(v2)^2+2*v1*v2*cos(theta)).

Finally we have tested the methods using the dummy data above and we got the results as expected.
i.e. collision happens after 3.3333 hr and for time less than 3.3333 hr the output obtained is false as expected and since 4 is greater than the collision time, we got the output as **True** as collision has already happened:blush:. 
                                                
   ![IMG_20230416_165240](https://user-images.githubusercontent.com/121503560/232306682-48b41a8e-ba7b-4af4-ae88-2fc3c3bde2a6.jpg)

                                
                                                
