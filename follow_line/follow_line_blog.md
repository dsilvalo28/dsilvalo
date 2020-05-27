Hi! 

In this blog I will try to explain how to get around a circuit with an autonomous car. For this we will use a simulator with all the tools we need, a car provided with an integrated camera and the circuit.

The instructions that we can give to the car are very simple, advance at x speed and turn left or right with x speed. We will use the camera integrated in the car to try to follow the red line that is in the middle of the circuit road. For this we will use a [PID controller](https://en.wikipedia.org/wiki/PID_controller).

In this case we will not take into account the integral controller, since good results have been observed only with PD controllers.

PID controllers, or PD in our case, are mainly focused on the error. In this example we will call the distance between the red line of the road and the center of our image an error. In order to anticipate turns on the circuit, we will measure this error at a safe distance from our car, more or less halfway up the horizon.

First of all, we have to locate the red line with our camera. For this, a color mask has been made in which only the red colors stand out. Once we have the black and white image only with the red line highlighted we can proceed to calculate our error.

The first thing is to know at what height we want to locate the red line, it does not have to be very close to the car in order to anticipate changes in the circuit, not too far away since we could lose the reference of the line in the circuit. For this, a height of 246 pixels has been chosen. Knowing the height at which we want to locate the line, we now have to find the center of that line. For this, the average occupied by the white pixels in our image is calculated. With the calculated center we subtract it from the center of our image and thus obtain the value of the error.

With the calculated error it is time to calculate the values ​​of kp and kd. These values ​​are calculated experimentally, trial and error. The values ​​will be modified until the car is able to be as above the red line as possible at all times.

Thanks to this, the objective of turning the circuit was achieved, in order to try to improve speed and precision, the following improvements were made.

[![](https://i.etsystatic.com/10919371/r/il/155a7d/1563938723/il_570xN.1563938723_1rmr.jpg)](https://youtu.be/5nlB7VrBZ8U)

I try to implement a controller that differentiates between curves and straights, to be able to go faster in curves. All the tests carried out were not satisfactory since in many of them the car ended up derailing and in others the time was not improved. For all this, this idea was rejected.

I hope it has helped you and I encourage you to try your own implementation!
