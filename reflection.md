# Describe the effect each of the P, I, D components had in your implementation

* **P**[roportional]:

  The proportional component of the controller ensures that the vehicle keeps on the reference track. In this case proportional means that the correction is proportional to the error (difference) between the desired state and the actual state. The proportional part alone, however, causes the vehicle to overshoot the target and causes the need for correction again, this time from the other side. This leads to an effect, where there vehicle initially oscillates around the target until the oscillations become smaller and eventually converge to the target.

* **D**[ifferential]:

  The differential component of the controller mitigates the shortcomings of an proportional-only controller by also considering the difference between the current error and the previous error, i.e. the differential of the error between two time steps. As the error becomes smaller over time the difference becomes negative because the previous error was larger than the current error. Adding this (negative) difference to the error creates a dampening effect, because the controller tries to correct a slightly smaller error term. The result is a smoothened control, which converges to the target track without or with considerably less oscillation.

* **I**[ntegral]:

  The integral component, as the name suggests, adds an integral over all calculated errors so far by summing all CTEs. This helps combating biases.

# Describe how the final hyperparameters were chosen

I experimented with the parameteres by manipulating them one by one and assessing their effect on the driving performance of the car in the simulator. I started off with the factors `Kp=0.1, Ki=0.05, Kd=1.0`. I increased the default speed of the car from `0.3` to `0.4` (~40mph).

I quickly realized that `Ki=0.05` was way too large. The car would go around in circles. I had to decrease all the way down to `Ki=0.001` for the car to drive correctly. `0.002` also worked, but the smaller value yielded more stable performance.

As for `Kp`, I only increased it slightly to `0.15`. For the lower speed of `0.3` `Kp=0.1` was good enough, but with the higher speed, the steering correction incentive needed to be slightly stronger.

`Kd` on the other hand, shouldn't be too large, as the dampening will prevent the vehicle from being able to pull away from the sides of the road. The performance didn't vary too much in the range of `2.0` ~ `8.0`, in the end I selected `3.0`.

