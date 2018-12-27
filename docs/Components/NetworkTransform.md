# NetworkTransform

The Network Transform component synchronizes the movement and rotation of GameObjects across the network. Note that the network Transform component only synchronizes spawned networked GameObjects.

![The Network Transform component](NetworkTransform.png)

-   **Network Send Rate (seconds)**  
    Set the number of network updates per second. You can set this slider to 0 for GameObjects that do not need to update after being created, like non-interactive effects generated by a player (for example, a dust cloud left behind that the player cannot interact with).
-   **Transform Sync Mode**  
    Select what type of synchronization should occur on this GameObject.
    -   **Sync None**  
        Don’t synchronize.
    -   **Sync Transform**  
        Use the GameObject’s Transform for synchronization. Use this if the physics system does not control this GameObject (that is, if you are moving it via scripting or animation). This is the default option.
    -   **Sync Rigidbody 2D**  
        Use the Rigidbody2D component for synchronization. Use this if the 2D physics system controls this GameObject.
    -   **Sync Rigidbody 3D**  
        Use the Rigidbody component for synchronization. Use this if the 3D physics system controls this GameObject.
    -   **Sync Character Controller**  
        Use the Character Controller component for synchronization. Only select this if you’re using a Character Controller.
-   **Movement:**
    -   **Movement Threshold**  
        Set the distance that a GameObject can move without sending a movement synchronization update.
    -   **Snap Threshold**  
        Set the threshold at which, if a movement update puts a GameObject further from its current position than this, the GameObject snaps to the position instead of moving smoothly.
    -   **Interpolate Movement Factor**  
        Use this to enable and control interpolation of the synchronized movement. The larger this number is, the faster the GameObject interpolates to the target position. If this is set to 0, the GameObject snaps to the new position.
-   **Rotation:**
    -   **Rotation Axis**  
        Define which rotation axis or axes should synchronize. This is set to XYZ (full 3D) by default.
    -   **Interpolate Rotation Factor**  
        Use this to enable and control interpolation of the synchronized rotation. The larger this number is, the faster the GameObject interpolates to the target rotation. If this is set to 0, the GameObject snaps to the new rotation.
    -   **Compress Rotation**  
        If you compress rotation data, the amount of data sent is lower, and the accuracy of the rotation synchronization is lower.
        -   **None**  
            Choose this to apply no compression to the rotation synchronization. This is the default option.
        -   **Low**  
            Choose this to apply a low amount of compression to the rotation synchronization. This option lessens the amount of information sent for rotation data.
        -   **High**  
            Choose this to apply a high amount of compression to the rotation synchronization. This option sends the least amount of information possible for rotation data.
        -   **Sync Angular Velocity**  
            Tick this checkbox to synchronize the angular velocity of the attached Rigidbody component.

This component takes authority into account, so local player GameObjects (which have local authority) synchronize their position from the client to server, then out to other clients. Other GameObjects (with server authority) synchronize their position from the server to clients.

A GameObject with a Network Transform component must also have a Network Identity component. When you create a Network Transform component on a GameObject, Mirror also creates a Network Identity component on that GameObject if it does not already have one.