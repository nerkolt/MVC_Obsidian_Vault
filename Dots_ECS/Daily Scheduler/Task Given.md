# Unity Wheel Colliders for MVC
* Fallback system lil entity when it's out of subscene => spawns wheel collider 
### vehicleTestSubScene
car entity uses entities wheel collider (bxb)

when entity(car05Entity) 5arjt mil subscene => VehicleTestScene : it falls
car05Entity
|__ Inputs
	 |__ Clutch
		 |__ Wheel brake
				 |__ Wheel

wheel authoring component mahoush yasn3 fi wheel collider lill 3jeli (wheels)
![[WheelAuthoring.png]]

![[wheelsChildren.png]]
![[wheeelCAuth.png]]

authoring is ready just add Wheel collider component 
![[WheelCollider.png]]
**HOW?**
Child object or same parent(same params as wcAuth)
only diff:
friction curve isn't the same:
extremum w adjacent values (evaluation for the curve)
**Go/monobehavior works only when subscene is closed**

