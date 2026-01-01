# Unity Wheel Colliders for MVC
* Fallback system lil entity when it's out of subscene => spawns wheel collider 
* So basically building a bridge between two different physics systems in our vehicle framework (ecs WC/unity WC)
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

## Basically
work on vehicleTestSubscene

# current architecture 
```bash
WheelAuthoring (MonoBehaviour on wheel GameObject)
    ↓
WheelNodeBaker (runs during SubScene baking)
    ↓
Creates: Wheel component (ECS data)
    ↓
Wheel.BridgeEntity → points to → WheelCollider entity (ECS physics)
```
## **The key components:**

- **WheelAuthoring**: The component you add to a wheel GameObject in the editor
- **WheelNodeBaker**: A "Baker" is like a compile-time converter - it runs during SubScene baking and transforms authoring data into ECS components
- **Wheel component**: Pure data struct in ECS that stores which wheel collider entity it should talk to
- **BridgeEntity**: Think of this as a pointer/reference - it's an `Entity` handle that connects the wheel logic to the physics entity

## Logic To follow
```
Is this GameObject inside a SubScene?
    YES → Use ECS wheel collider (existing behavior)
    NO  → Fall back to Unity's WheelCollider MonoBehaviour
```
