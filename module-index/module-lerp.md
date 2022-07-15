# Linear Interpolation


>**Alias:** `lerp`  
>**Contract Name:** `dss-lerp`  
>**Scope:** One instance for each parameter  
>**Technical docs:**  

## Description

The Linear Interpolation Module (`lerp`) allows a governance parameter to be changed linearly over a fixed period of time. 

## Purpose

The primary purpose of the `lerp` module is to enable Governance to change a parameter gradually using only a single executive vote. The duration over which the parameter is changed, the starting value, and final value of the parameter can be chosen for each instance of the lerp module.

## Execution 
The `lerp` contract has one method called tick(), which is permissionless and can be called by anyone. This updates the target parameter to be whatever value it should be at that moment. If the elapsed time is longer than the duration, calling tick() will finish the `lerp` by changing `done` to true and set the parameter to the end value. 


## Key Parameters

Each `lerp` factory invocation creates a new contract which has the following properties:

### target 
The target contract in which a parameter is being changed. 

### what 
The name of the parameter being changed. 

### startTime 
The starting time of this lerp instance. 

### start 
The starting value of that parameter. 

### end 
The ending value of that parameter. 

### duration 
The duration over which this lerp instance will run for. 

### done
This refers to whether the given `lerp` instance is finished or not.



## Trade-offs

Typically, the start and end parameters are adjusted to represent the current state and the desired state for the protocol. Hence, a longer `duration` results in the parameter being suboptimal for a longer period of time. On the other hand, more gradual changes are desirable as the protocols users can adapt more easily.


## Considerations

When `lerp` is used to determine allocation of protocol earnings, such as setting the System Surplus Buffer, Governance should ensure that the desired rate of increase is not larger than the expected protocol earnings. If the desired rate is too high, the `lerp` has no effect. 

>Page last reviewed: -
>Next review due: -

