# Guide to Flying Cool Planes
## Table of Contents
- [Some Basic Knowledge](#Some Basic Knowledge)
- [Binding](#Binding)
- [Servo Testing](#Servo Testing)
- [Transmitter & Mission Planner Setup](#Transmitter & Mission Planner Setup)
- [Flight Mode Setup](#Flight Mode Setup)
  - [Fly By Wire_A (FBWA)](#FBWA)
  - [Fly By Wire_B (FBWB)](#FBWB)
  - [Loiter](#Loiter)
  - [Circle](#Circle)
  - [Return to Launch (RTL)](#RTL)
  - [Auto](#AUTO)

- [Sensor Setup](#Sensor Setup)
  - [Airspeed Sensor](#Airspeed Sensor)
- [Failsafe](#Failsafe)

<div id='Some Basic Knowledge'/>
## Some Basic Knowledge
- **What is Mission Planner? What is a transmitter?**

 Mission Planner is the software we use to monitor sensors and perform autonomous tasks and flight modes with the plane. [More info here](http://ardupilot.org/planner/docs/mission-planner-overview.html). A transmitter is that cool thing with joysticks that we use to control the planes manually. **We highly recommend that you practice with a transmitter and simulator first before flying any actual planes.**
- **Control Surfaces**

 These are the things that control the plane's movement or attitude. They are called the ailerons, elevator, and rudder, which control roll, pitch, and yaw, respectively. Roll, pitch, and yaw are rotation about the x, y, and z axes. [Here's a diagram.](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c1/Yaw_Axis_Corrected.svg/2000px-Yaw_Axis_Corrected.svg.png)
- **What is 'trim'?** (You'll see this mentioned in Transmitter Setup)

  First, you should know that the servos controlling the control surfaces have a range of PWM signals they respond to. For example, the minimum PWM signal for the elevator could point it all the way down, and the max could point it all the way up. Trim is a way of adjusting the placement of this range so the middle value is in the correct place. However, this also adjusts the placement of the min amd max values, which limits the range of the control surface (Ex: If the min PWM signal is raised, the elevator can't point all the way down). So, if the control surface is off by a little bit, go ahead and adjust it with trim. If it has a major offset (like the elevator is pointing down when it should be in the middle), adjust the servo connection manually. (As a side note, when setting the trim in Transmitter Setup, it's changing the PWM signals for non-control surface channels, giving the channels involved 6 options instead of 9. Trim's purpose is less straightforward).

- **Flight mode parameters** (the weird words in all caps) 

 These control various things about autonomous flight modes and failsafes. They can be found in Mission Planner under the top CONFIG/TUNING tab, and then under "Advanced Params" in the sidebar.

<div id='Binding'/>
## Binding

<div id='Servo Testing'/>
## Servo Testing

<div id='Transmitter & Mission Planner Setup'/>
## Transmitter & Mission Planner Setup
**It is critical that you follow this correctly, otherwise control surfaces could reverse in different flight modes**

- link: [Servo and Transmitter Configuration](http://ardupilot.org/plane/docs/reversing-servos-and-setting-normalelevon-mode.html)

<div id='Flight Mode Setup'/>
## Flight Mode Setup

<div id='FBWA'/>
### Fly By Wire_A (FBWA)
[http://ardupilot.org/plane/docs/fbwa-mode.html](http://ardupilot.org/plane/docs/fbwa-mode.html)  
Plane holds the roll and pitch specified by the control sticks. So if you hold the aileron stick hard right then the plane will hold its pitch level and will bank right by the angle specified in the LIM_ROLL_CD option (in centidegrees).  Note that holding level pitch does not mean the plane will hold altitude. If you want Plane to take care of holding altitude then you should look at the FBWB mode.

<div id='FBWB'/>
### Fly By Wire_A (FBWB) **UNTESTED**
[http://ardupilot.org/plane/docs/fbwb-mode.html#fbwb-mode](http://ardupilot.org/plane/docs/fbwb-mode.html#fbwb-mode)
The FBWB mode is similar to FLY BY WIRE_A (FBWA), but Plane will try to hold altitude as well. Roll control is the same as FBWA, and altitude is controlled using the elevator. The target airspeed is controlled using the throttle.

<div id='Loiter'/>
### Loiter
[http://ardupilot.org/plane/docs/loiter-mode.html](http://ardupilot.org/plane/docs/loiter-mode.html)

In LOITER mode the plane will circle around the point where you started the loiter, holding altitude at the altitude that you entered loiter in.

1. WP_LOITER_RAD
2. NAV_ROLL_CD
3. NAVL1_PERIOD
4. Altitude?

<div id='Circle'/>
### Circle
Circle mode is similar to LOITER, but doesn’t attempt to hold position. Circle mode is deliberately a very conservative mode, and doesn’t rely on GPS positioning as it is used when GPS fails.  If you want the plane to fly in circles, use [loiter](#Loiter) mode.

<div id='RTL'/>
### RTL

<div id='AUTO'/>
### AUTO

<div id='Sensor Setup'/>
## Sensor Setup
<div id='Airspeed Sensor'/>
### Airspeed Sensor

<div id='Failsafe'/>
## Failsafe
http://ardupilot.org/plane/docs/apms-failsafe-function.html

1. Set FS_GCS_ENABL to 1 to enable it.
2. Connect to the Mission Planner via telemetry. Verify on the bottom right corner of the HUD that you are “flying” in a non auto mode (Manual, Stabilize, FBW are ok).
3. Unplug one of the telemetry radios. After a few minutes power off your autopilot. (Remember the autopilot will not go into failsafe until FS_LONG_TIMEOUT seconds of MAVlink inactivity have passed).
4. Connect your autopilot to the mission planner and pull the logs. Verify on the log that the autopilot went into RTL after FS_LONG_TIMEOUT sec of MAVlink inactivity.
5. FS_SHORT_TIMEOUT: 1
6. FS_SHORT_ACTN: 0
7. FS_LONG_TIMEOUT: 5
8. FS_LONG_ACTN: 1
