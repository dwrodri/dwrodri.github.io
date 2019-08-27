# Walking through everything that happens when the first scene is loaded in RPD

##  inside main()
1. main() is called, and the JSON parser fetches the file passed in argv[1] 
2. The singleton containing the core game loop (EngineCore) is instantiated, and passed the "engine\_core" chunk of the JSON blob.
3. The EngineCore singleton kicks off the game loop by calling the Run() function.

## Inside EngineCore.Run()

4. Once inside the Run() function, more singletons are spawned: Clock, RenderManager, InputManager, and PhysicsCore
5. The Clock singleton is started with its Start() function.
6. The first Scene--called `current_scene` is instantiated in the EngineCore. This Scene instanced is wrapped in a `std::unique_ptr`.
7. `current_scene` is configured by calling the configure() function, which is passed EngineCore's `initial_scene` member.
8. A `std::queue` is created for the input data from a controller/keyboard/etc.
9. The main game loop inside the EngineCore is entered. The loop exit logic is based on a bolean called `running`.
10. **The input queue is assigned to be the output of the InputManager singleton's HandleInput() function**
11. The game loop performs a check to see if there's an exit signal at the back of the input queue. If so, the clock is stopped, and the loop is exited.
12. Assuming no exit signal, we collect the number of elapsed ticks from the Clock singleton.
13. `current_scene` is handed the input queue through the HandleInput function.
14. If there this isn't the very first game tick(), we enter anothe control block where we delegate work to change game state.
15. The `current_scene` instance calls its UpdateAll function, and recieves the number of ticks.
16. The PhysicsCore singleton calls its CheckCollisions function, which receives the Actors, Props, and Stage from `current_scene`.
17. We exit the control block checking for the first game tick, and tell the RenderManager singleton to clear the previous frame SDL Renderer.
18. `current_scene` calls the RenderAll() function, generating the next frame's worth of content for the RenderManager singleton.
19. RengerManager's SceneToScreen() function is called, pushing that frame into the window. 
20. The core game loop ends.

## Exiting Engine.Run(), back inside main()

21. main() calls EngineCore's Cleanup() function.
22. The program exits.

