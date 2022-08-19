# Fuel Level

## Introduction

This example demonstrates how to specify a software and to implement it by using a modular architecture.

## Natural Language Description

We are considering to estimate the remaining amount of fuel in a tank. This information is critical for a plane, for example, because an error in the estimation might lead to a crash.

So we would like to develop a piece of software that would make the pilot aware of the situation (fuel level below a given capacity). This is in fact the main property of our software, independently from the way the fuel level is estimated.

As the sensors are likely to provide inaccurate / erroneous measures, the architecture of the system includes redundancy (2 ultrasonic level sensors, 3 flowmeters) and the estimation of the furel left in the tank is performed in two steps:

* initial level in the tank is estimated with the 2 ultrasonic level sensors (minimum value of the two measures)
* each cycle, current level is estimated by substracting the maximum value given by the 3 flowmeters)

When the estimated level is less or equal to a given value, an alarm is raised.

## Formal specification

The resulting modelling contains 7 files:

* fuel0 is the top level specification of our software.
* fuel\_i is its implementation, that requires services from measure and utils
* measure is a basic machine, in charge of acquiring data from sensors. This component is implemented manually.
* utils is a stateless machine offering 2 services: minimum of 2 NATURAL numbers, maximum of 3 NATURAL numbers.
* utils\_i is its implementation
* ctx contains the definition of constants
* ctx\_i is its implementation. The values of the constants are provided, in order to be checked against their properties. Constants are then demonstrated to be implementable.

The machine fuel0 contains two operations:

* compute\_initial\_level: initial estimation of the amount of fuel in the tank
* compute\_remaining\_fuel: called repeatidly to estimate consumption and remaining fuel

The main property of this component is: (estimated\_level <= WARNING\_CAPACITY => status = LOW\_LEVEL)

The variable status is used to raise an alarm.



```
MACHINE fuel0
SEES
   ctx
VARIABLES
   estimated_level,
   estimated_consumption,
   status
INVARIANT
   /* Typing */
   estimated_level : 0..TANK_CAPACITY &
   estimated_consumption : 0 ..MAX_CONSUMPTION &
   status : tSTATUS &
   /* Security property */
   (estimated_level <= WARNING_CAPACITY => status = LOW_LEVEL)
INITIALISATION
   estimated_level := 0 ||
   estimated_consumption := 0 ||
   status := LOW_LEVEL
OPERATIONS
   compute_initial_level =
   BEGIN
       estimated_level, status :(
           estimated_level: 0..TANK_CAPACITY &
           status : tSTATUS &
           (estimated_level <= WARNING_CAPACITY => status = LOW_LEVEL))
   END
;
   compute_remaining_fuel =
   BEGIN
       estimated_level, estimated_consumption, status :(
           estimated_level: 0..TANK_CAPACITY &
           estimated_consumption : 0..MAX_CONSUMPTION &
           status : tSTATUS &
           (estimated_level <= estimated_level$0) &
           (estimated_level <= WARNING_CAPACITY => status = LOW_LEVEL))
   END
END
```

This implementation fuel\_i implements the two operations defined in fuel0, and imports services from measure and utils.

```
IMPLEMENTATION fuel_i
REFINES fuel0
SEES ctx
IMPORTS
   measure,
   utils

CONCRETE_VARIABLES
   estimated_level ,
   estimated_consumption ,
   status

INITIALISATION
   estimated_level := 0 ;
   estimated_consumption := 0 ;
   status := LOW_LEVEL

OPERATIONS
   compute_initial_level =
   VAR m1, m2 IN
       m1, m2 <-- measure_level;
       estimated_level <-- minimum(m1, m2);
       IF estimated_level <= WARNING_CAPACITY
       THEN
           status := LOW_LEVEL
       ELSE
           status := NOMINAL
       END
END
;
   compute_remaining_fuel =
   VAR m1, m2, m3 IN
       m1, m2, m3 <-- measure_consumption;
       estimated_consumption <-- maximum(m1,m2,m3);
       IF estimated_consumption >= estimated_level 
       THEN
           estimated_level := 0
       ELSE
           estimated_level := estimated_level - estimated_consumption
       END;
       IF estimated_level <= WARNING_CAPACITY
       THEN
           status := LOW_LEVEL
       END
   END
END
```

The component measure provides two services: measure\_level and measure\_consumption. These two operations have to be developped manually.

```
MACHINE measure
SEES ctx

OPERATIONS
   m1, m2 <-- measure_level =
   BEGIN
       m1 :: 0..TANK_CAPACITY ||
       m2 :: 0..TANK_CAPACITY
   END;

   m1, m2, m3 <-- measure_consumption =
   BEGIN
       m1 :: 0..MAX_CONSUMPTION ||
       m2 :: 0..MAX_CONSUMPTION ||
       m3 :: 0..MAX_CONSUMPTION
   END
END
```

The component utils provides two services: minimum and maximum.

```
MACHINE utils

OPERATIONS
   rr <-- minimum(aa, bb) =
   PRE
       aa: NAT &
       bb: NAT
   THEN
       rr := min({aa, bb})
   END;

   rr <-- maximum(aa, bb, cc) =
   PRE
       aa: NAT &
       bb: NAT &
       cc: NAT
   THEN
       rr := max({aa, bb, cc})
   END
END
```

The component utils\_i implements the two services defined in utils

```
IMPLEMENTATION utils_i

REFINES utils

OPERATIONS
   rr <-- minimum ( aa , bb) =
   BEGIN
       IF aa >= bb
       THEN
           rr := bb
       ELSE
           rr := aa
       END
   END
;
   rr <-- maximum ( aa , bb , cc ) =
   BEGIN
       IF aa >= bb
       THEN
           IF aa >= cc THEN
               rr := aa
           ELSE
               rr := cc
           END
       ELSIF bb >= cc THEN
           rr := bb
       ELSE
           rr := cc
       END
   END
END
```

The component ctx contains the constants of the software.

```
MACHINE ctx

SETS
   tSTATUS = {NOMINAL, LOW_LEVEL}

CONSTANTS
   TANK_CAPACITY,             /* max quantity of fuel in the tank */
   MAX_CONSUMPTION,     /* max quantity of fuel consumed in a cycle */
   WARNING_CAPACITY     /* low fuel level */

PROPERTIES
   TANK_CAPACITY : NAT1 &
   MAX_CONSUMPTION : NAT1 &
   WARNING_CAPACITY : NAT1 &
   MAX_CONSUMPTION < TANK_CAPACITY &
   WARNING_CAPACITY < TANK_CAPACITY
END
```

The component ctx\_i contains the values of the constants.

```
IMPLEMENTATION ctx_i
REFINES ctx

VALUES
   TANK_CAPACITY = 1000;
   MAX_CONSUMPTION = 10;
   WARNING_CAPACITY = 100
END
```

## Populating the Project

Once the project is created (software development), add the various machines starting with ctx, utild, measure, then fuel0. Then create the implementations. Each time, create the component empty then copy-paste the contents from this page.&#x20;

Once all the components are in the project:&#x20;

* generate the proof obligations (button Po on the toolbar)
* execute the proof in force 0 (button F0 on the toolbar)
* execute the proof in force 1 (button F1 on the toolbar)

You should obtain the following status below from the Top-Bottom graphical view. The color green indicates that the components are fully proven.

![Project structure: the lines are decomposition links (fuel\_i imports measure and utils components)](../.gitbook/assets/fuel-level-project-structure.jpg)

