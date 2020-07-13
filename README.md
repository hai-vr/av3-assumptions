The following are my current assumptions about Avatars 3.0.

Confidence levels is how sure I believe I am about a statement.

- 100%: Almost certain
- 75%: Pretty sure
- 50%: Probably
- 25%: I haven't tested it much
- 0%: I have been told but have not verified

## VRChat SDK

### Playable layers

- Locomotion layer, Additive layer, Gesture layer, Action layer can only change:
  - Transforms *(confidence 100%)*
  - Muscles *(confidence 100%)*
  - GameObject toggles *(confidence 75%)*

- **Locomotion layer** should only be for the movement animations of the avatar *(confidence 75%)*
  - OPINION: You should duplicate the example VRChat Action animator and edit it rather than create one from scratch *(confidence 100%)*

- **Additive layer** should only be for tiny subtle movements such as breathing *(confidence 25%)*
  - Transforms modified by the additive layer are completely overridden by the Playable layers that are below it, meaning Gesture layer and Action layer *(confidence 0%)*

- **Gesture layer** should be for anything that changes a portion of bone movement *(confidence 25%)*
  - The base mask of the Gesture layer needs to be the sum of all the masks below it *(confidence 25%)*
  - It is not necessary for the mask to include non-humanoid objects which would have been animated by the Gesture layer *(confidence 0%)*
  - OPINION: The word Gesture refers to its original meaning: it does NOT mean face expressions, but finger positions *(confidence 100%)*

- **Action layer** should be for animations that override the movement of all or almost all the avatar *(confidence 25%)*
  - By default, the action layer weight will be 0 *(confidence 100%)*
  - OPINION: You should duplicate the example VRChat Action animator and edit it rather than create one from scratch *(confidence 100%)*

- **FX layer** should be for animating anything that is not a transform nor a muscle *(confidence 75%)*:
  - Examples of non-transforms are:
    - GameObject toggles *(confidence 100%)*
    - Blend shapes *(confidence 100%)*
    - Material properties *(confidence 100%)*
    - Constraint weights *(confidence 100%)*
    - Material swapping *(confidence 75%)*
    - Animator Behaviors *(confidence 75%)*

- OPINION: Unless you actively want to change a Playable layer to make active use of them, try to leave the Locomotion and Action playable layers to the defaults, **especially the Locomotion layer**. That way, it will default to the VRChat provided defaults, which may update over time. *(confidence 25%)*

## Unity specific

### Blend trees

- OPINION: If an animation of a blend tree animates a property, then every animation of that blend tree should also animate that property back to the defaults if unused *(confidence 75%)*
  - *REASONING: When MissStabby created her complex blend tree, swiping quickly to another coordinate would yield different results every time, which were visible both in the Unity editor and in-game. This opinion was forged during a conference call with MissStabby and a VRChat developer*


## Unity Editor specific

### Unity Editor gotchas

- When creating a layer, the layer will have a weight of 0 by default *(confidence 100%)*
  - OPINION: You should change it to 1 in most of the cases *(confidence 100%)*

- On a transition, changing the parameter of a condition will reset the comparison operator no matter what *(confidence 100%)*

- In play mode, editing the animator controller states and transitions will save them *(confidence 75%)*
  - In play mode, editing the behaviors of a state will NOT save them *(confidence 100%)*
  - In play mode, editing the layer weight will NOT save them *(confidence 100%)*

- If the OS is in French, whenever blend trees values are edited by hand, the comma decimal separator must be manually changed to a dot for the change to take effect *(confidence 75%)*
