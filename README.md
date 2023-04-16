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
    # calculates the distance between this car and another car
        dx = self.x - car2.x
        dy = self.y - car2.y
        return math.sqrt(dx*dx + dy*dy)
    
    def collision_possibility(self,car2):
    #Here we calculate the direction of relative velocity and see whether the other car is in that direction or not.
        if(math.atan((car2.y-self.y)/car2.x-self.x) == math.atan2(self.speed * math.sin(math.degrees(self.direction))-car2.speed * math.sin(math.degrees(self.direction)),
                                                                self.speed * math.cos(math.degrees(self.direction))-car2.speed * math.sin(math.degrees(car2.direction))):
               return true
        else: 
               return false
               
    def detect_collision(self,car2,curent_time):
        if(collision_possibility(self,car2) and current_time > time_to_collision(self, other)):
              return true
        else
              return False
               
    def time_to_collision(self, other):
    # calculates the time until this car collides with another car
        v_rel = math.sqrt(self.speed*self.speed+car2.speed*car2.speed+2*self.speed*car2.speed*math.cos(math.degrees(self.direction))
        Time_to_collision =  distance(self, car2)/v_rel
 __________________________________________________________________________________________________________________________________________________________________________    
     
******example test cases of the Car class for the methods with dummy data:******

car1 = Car("Hyundai", "Creta", 2022, 50, 0, 0)
car2 = Car("Maruti", "Swift", 2021, 40, 100, 0)

car1.accelerate(10)
car1.move()

car2.accelerate(5)
car2.move()

print(car1.detect_collision(car2))    # False
print(car1.time_to_collision(car2))   # 3.3333333333333335 seconds

____________________________________________________________________________________________________________________________________________________________________

**************I have also included the code above itself for convenience**************
                                               
                                               <ins>DECONSTRUCTING THE ABOVE CODE</ins>
                                                
                                                
                                                
