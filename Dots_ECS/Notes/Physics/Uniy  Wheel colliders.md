[source](https://www.youtube.com/watch?v=c-yhZwXSx_c)

![[wheelColliderComponent.png| 350]]
* Mass:extra mass with rigidbody
* wheelDampingrate : when the "power" transfers from wheel to car the spring damps down some extra strength to make it smooth when there's a bump for example

![[Wheel.png]]
Appllied point : where force is applied in the car
![[SuspensionForcze.png]]
unity takes pos of wheel + distance of spring = controlled by applied point
* suspension spring  F=k*x : k is spring , damper for loss force ,target pos of the spring % wheel
* Forward / sideways friction : F = μ*N
object not moving vs slipping ? : force applied if it's slipping is a lot lower than if it's not moving 
![[frictionCurve.png]]
![[FrictionAnalysis.png]]

Stiffness : change force applied depending on terrain (grass,concrete,ice...) higher the bigger friction => less sliding wheel
forward friction high for movement side friction lower for sliding 