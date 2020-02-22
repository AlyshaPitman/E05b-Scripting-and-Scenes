# E05b-Scripting-and-Scenes

To continue to prepare you to turn in the space shooter project, we will experiment a little with more scripting, some procedural generation, and switching scenes in GDScript.

- This was a part of the project I had trouble with. Specifically, the program wanted to reject the if statement " if position.y > get_viewport_rect().end.y:" 

 * Edit the script attached to the Ball node (res://Scripts/ball.gd):
 ```
 extends RigidBody2D
 
 export var maxspeed = 300
 
 signal lives
 signal score
 
 func _ready():
  contact_monitor = true
  set_max_contacts_reported(4)
  var WorldNode = get_node("/root/World")
  connect("score", WorldNode, "increase_score")
  connect("lives", WorldNode, "decrease_lives")
 
 func _physics_process(delta):
  var bodies = get_colliding_bodies()
  for body in bodies:
   if body.is_in_group("Tiles"):
    emit_signal("score",body.score)
    body.queue_free()
   if body.get_name() == "Paddle":
    pass
   
  if position.y > get_viewport_rect().end.y:
   emit_signal("lives")
   queue_free()
 ```
 
If you have score and lives labels that update, and if you get a end-game screen if your lives get to zero, you have completed the exercise. Save the Scenes, edit your LICENSE and README, commit everything to Github, and turn in the URL of your repository on Canvas.
 
