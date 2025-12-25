# Stateless vs stateful system

State refers to the physical properties of  a system at a given time (e.g state of gaz is characterised by volume,pressure,Temp.. ) vs stateless which current state doesn't depend on previous state.Future behavior is determined entirely by its current state  
#### Example:
* e.g ball rolling down a hill that picks up speed and eventually comes to a stop ;; once stopped the ball's state (speed,position...)doesn't depend it rolled... (something could've affected its state while rolling yet it doesn't directly affect th stop state of the ball )
* ball rolls down a hill => picks up speed => current state of velocity depends on previous state(top of hill for example ) it'll be diff depending on how it rolled from top (slightly/forcefully pushed)

Havok is a stateful physics engine ; advantage is ability to simulate large num. of objects with minimal overhead 