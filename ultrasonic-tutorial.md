### @explicitHints true

# :MOVE Motor Ultrasonic Sensor

## Introduction @unplugged
Learn how to use the :MOVE Motor's Ultrasonic Distance Sensor to detect objects and stay a certain distance from them.

![:MOVE Motor front view](https://KitronikLtd.github.io/pxt-kitronik-move-motor/assets/move-motor-front.jpg)

## Step 1
Start by creating a variable called ``||variables:distance||`` and place the ``||variables:set distance to||`` block in the ``||basic:forever||`` loop.  

Make ``||variables:distance||`` equal to ``||Kitronik_Move_Motor.measure distance||`` by dropping the block inside (this can be found in the ``||Kitronik_Move_Motor.Sensors||`` section of the ``||Kitronik_Move_Motor.MOVE Motor||`` category).

#### ~ tutorialhint
```blocks
let distance = 0
basic.forever(function () {
    distance = Kitronik_Move_Motor.measure()
})
```

## Step 1
From the ``||logic:logic||`` drawer, add an ``||logic:if||`` statement at the bottom of the forever block. Also from the ``||logic:logic||`` drawer, place ``||logic:0 < 0||`` into the top of the if block.  

In the place of the first 0, put a ``||variables:distance||`` bubble from the ``||variables:variables||`` drawer, change the ``||logic:<||`` to be ``||logic:>||``, and change the second 0 to 10.  

#### ~ tutorialhint
```blocks
let distance = 0
basic.forever(function () {
    distance = Kitronik_Move_Motor.measure()
    // @highlight
    if (distance > 10) {
    }
})
```

## Step 1.5
Inside the opening of the ``||logic:if||`` block, place a ``||Kitronik_Move_Motor.move forward at speed 0||`` block. This block will run if the condition is met.  

Set the speed to 30.

#### ~ tutorialhint
```blocks
let distance = 0
basic.forever(function () {
    distance = Kitronik_Move_Motor.measure()
    if (distance > 10) {
        // @highlight
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 30)
    }
})
```

## Step 2
This means the motors start as soon as an obstacle is more than 10cm away, but they never stop, so the :MOVE motor will just keep going. 
We need to stop when we get too close to an obstacle.  

Click the ``||logic:+||`` icon to add an ``||logic:else||`` statement and place a ``||Kitronik_Move_Motor.stop||`` block inside.

#### ~ tutorialhint

![Animation that shows how to add an else statement](https://KitronikLtd.github.io/pxt-kitronik-move-motor/assets/add-else-statement-stop.gif)

```ghost
let distance = 0
basic.forever(function () {
    distance = Kitronik_Move_Motor.measure()
    if (distance > 10) {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 30)
    } else {
        // @highlight
        Kitronik_Move_Motor.stop()
    }
})

```

## Step 4
If you have a @boardname@ connected, click ``|Download|`` to transfer your code and switch on :MOVE Motor. 
Place a box in front of the :MOVE Motor and see it follow as the box is moved away, but it stops when it gets within 10cm. 

## Free Roaming @unplugged
### Free Roaming
Great! The :MOVE Motor can now move forwards, but it can only move in a straight line. It would be much better if it could drive around by itself and not crash into things...

## Step 5
Click the ``||logic:+||`` icon on your existing ``||logic:if||`` block to add an ``||logic:else if||`` statement. 
Put in ``||variables:distance||`` ``||logic:< 10||`` as the test condition.

#### ~ tutorialhint
```blocks
let distance = 0
basic.forever(function () {
    distance = Kitronik_Move_Motor.measure()
    if (distance > 10) {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 30)
    // @highlight
    } else if (distance < 10) {

    } else {
        Kitronik_Move_Motor.stop()
    }
})
```

## Step 1
Move the ``||Kitronik_Move_Motor.stop||`` block from its current location up to the space in the ``||logic:else if||`` section. 
Directly below the ``||Kitronik_Move_Motor.stop||`` add a ``||Kitronik_Move_Motor.move forward at speed 0||`` block, then change **forward** to **reverse**. Set the speed to 30.  

Then, click the ``||logic:-||`` icon on the empty ``||logic:else||`` statement to remove it.

#### ~ tutorialhint
```blocks
let distance = 0
basic.forever(function () {
    distance = Kitronik_Move_Motor.measure()
    if (distance > 10) {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 30)
    } else if (distance < 10) {
        Kitronik_Move_Motor.stop()
        // @highlight
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Reverse, 30)
    }
})
```

## Step 2
Next, add a 500ms ``||basic:pause||`` from the ``||basic:basic||`` drawer after the ``||Kitronik_Move_Motor.stop||``, and a 1 second ``||basic:pause||`` after the ``||Kitronik_Move_Motor.reverse||`` block.

#### ~ tutorialhint
```blocks
let distance = 0
basic.forever(function () {
    distance = Kitronik_Move_Motor.measure()
    if (distance > 10) {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 30)
    } else if (distance < 10) {
        Kitronik_Move_Motor.stop()
        basic.pause(500)
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Reverse, 30)
        basic.pause(1000)
    }
})
```

## Step 3
We need to make :MOVE Motor turn away from the obstacle it has detected. 
Add a ``||Kitronik_Move_Motor.spin left at speed 0||`` block to the botom of the ``||logic:else if||`` section, followed by a 300ms ``||basic:pause||`` and a ``||Kitronik_Move_Motor.stop||`` block.  

Change the spin speed to 50.

#### ~ tutorialhint
```blocks
let distance = 0
basic.forever(function () {
    distance = Kitronik_Move_Motor.measure()
    if (distance > 10) {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, 30)
    } else if (distance < 10) {
        Kitronik_Move_Motor.stop()
        basic.pause(500)
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Reverse, 30)
        basic.pause(1000)
        Kitronik_Move_Motor.spin(Kitronik_Move_Motor.SpinDirections.Left, 50)
        basic.pause(300)
        Kitronik_Move_Motor.stop()
    }
})
```

## Step 4
Finally, add a 500ms ``||basic:pause||`` after the stop block.

CODING COMPLETE! If you have a @boardname@ connected, click ``|Download|`` to transfer your code and switch on :MOVE Motor. 
Now put :MOVE Motor on the floor and watch it roam around avoiding obstacles.

```package
loops
input
variables
logic
kitronik-move-motor=github:KitronikLtd/pxt-kitronik-move-motor
```