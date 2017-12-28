# PID Project

# Approach
My approach to tuning the PID controller was to iteratively tune the P, I, and D
parameters by hand in succession until a decent performance we achieved. So I 
essentially started with a P only controller, then a PD controller, then a PID
controller. Then I manually twiddled the values to fine tune.

## P Controller
To find a good initial P value, I looked for a value that gave an sufficient
time response to the changes in the road. I.e., the controller should be able 
to make the car turn fast enough to round the corners. This is the effect of the
P parameter, controlling how fast the filter acts to correct error.

This still has the problem that controller can overshoot, and then cause 
oscillations. This is seen in the video below. Eventually this causes the car to
go off the track.

<video controls src='P.mp4' width=480/>

## PD Controller
The D parameter tends to act against change in the error. This can be used to 
dampen out the oscillations found in the P only controller. 

The PD controller still has the problem that it tends to understeer in the 
corners ending up on the outside of the lane.
<video controls src='PD.mp4' width=480/>

## PID Controller
The I parameter tends to act against the total error the controller has seen.
This can in effect also learn an bias in the process model. In the simulation,
a bias happens when turning a corner. The car must steer at a steady non-zero
angle to go around a corner. This helps correct the understeering in the PD
controller.

## Final Controller
I also added a throttle controller that reduces the throttle when the car is 
turning. This mimics real driving behavior and makes the whole system perform
a bit better in the tight corners. Ideally, you would slow down *before*
entering the turn, but this controller does not know about the upcoming road
state.