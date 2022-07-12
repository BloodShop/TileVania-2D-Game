# TileVania-2D-Game
TileVania-2D-Game MVP Gameplay

![image](https://user-images.githubusercontent.com/23366804/178499941-c9651e7a-a262-4fc7-be8d-3dcc3a70ad6a.png)

# TileVania Game Design
Player Experience: Under pressure
Core Mechanic: Run and jump
Core game loop: Get from A to B by navigating platforms and avoiding traps and enemies 

![image](https://user-images.githubusercontent.com/23366804/178502204-8d44de97-09b9-456c-892a-4bdd2f32dc98.png)

# MVP Gameplay Features
** Character movement: Player can run and jump
** Traps / obstacles: Instantly kill the player
** Level loading: A way to finish the level and start next level
** Countdown timer: Some system to create time urgency

# Tilemap Pipeline
------->------->------->------->------->------->------->------->------->------->
*Sprite Sheet --> Sliced Sprite --> Tile Asset --> Tile Palette --> Tilemap (scene)
------->------->------->------->------->------->------->------->------->------->

# Terminology
** Animator Component - Assigns animations to GameObjects through an Animator Controller
** Animator Controller - Arrangement of animations and transitions (state machine).
** Animation - Specific pieces of motion
** Sprite Renderer - displays the 2D sprite on screen

![image](https://user-images.githubusercontent.com/23366804/178502476-7c8029a8-4146-446d-a329-e84efd96ec9d.png)

# What Are Prefabs
** Prefabs are game objects which we have turned into reusable templates
** The original template is called the Prefab and the copies we add into our scene are called Instances 
** Turning a game object into a prefab means we can easily load it into any scene in our game

# Flippin’ Logic
** If the player is pushing right, the velocity will be positive. If left, then negative.
** If moving right, we should face right. If left, face left.
** We can change the facing direction (right or left) by changing the localscale using +ve or -ve value.
** Only change facing direction if moving, so weird things don’t happen when velocity is zero.

# Layers
** Layers are useful if we have the same functionality across multiple GameObjects.
Eg. Ignored by camera, not clickable, collision check

** To stop jumping anytime we use *Collider2D.IsTouchingLayers()

![image](https://user-images.githubusercontent.com/23366804/178502700-61319a3c-d8ed-4267-9651-0af8f4403820.png)

# Coroutines Explained
** Coroutines are another way for us to create a delay in our game. 
** The core concept to understand is that we start a process (ie. Start Coroutine) and then go off and do other things (ie. Yield) until our condition (eg. we’ve waited 2 seconds) is met.

  **Coroutines Code**
- We call: 
StartCoroutine(NameOfMethod());
- Our method:
IEnumerator NameOfMethod()
{
		yield return new WaitForSecondsRealtime(time);
		// Anything you want to do after waiting
}

# Our Goal
1. Player has X lives
2. Restart scene when player dies
3. When all lives are lost, game over
4. Restarting the game resets lives and score.
  **- The Problem**
** After death, reloading the scene re-instantiates the Player, and all other objects.
** Any progress with the player or scene is lost.
