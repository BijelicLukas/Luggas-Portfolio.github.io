[<--- Back to main Page](./index.md)
# Last Response
Last Response is a solo GameJam project made in Unity for the theme **“Lost Signal.”**  
The player monitors nine rooms through a phone system, listening to ambient sounds and deciding whether each room is safe or needs to be terminated. Different enemy types affect the soundscape in unique ways, from simple threats that emit periodic noises to a chainsaw enemy that drowns out other signals and a “faker” that mimics room responses through pitch changes.  
I focused on the enemy behavior logic, the room and state management, and the UI that lets the player quickly read room status and trigger termination under time pressure.

---

# Challenges

- Designing a room system for nine rooms that could track states such as idle, threatened and terminated, while still being easy to control from code.  

- Implementing multiple enemy types with distinct behavior patterns (periodic threats, constant noise, fake responses) that all interact with the same room system.  

- Making sure enemies never occupied the same room at the same time while still feeling random and unpredictable.  

- Building a UI that clearly represented all nine rooms, including a “termination mode” that changed button colors and states to show which rooms were shut down.  

- Creating an audio-driven experience where the player relies on sound direction, timing and pitch changes to read threats without the game becoming unreadable noise.

---

## Solutions

- Introduced a `RoomManager` with separate components for room data and logic, so each room could track its current state and respond consistently to player input and enemy events.  

- Created individual enemy scripts plus a simple spawn system that assigns enemies to free rooms, rerolling if a room is already occupied to avoid overlapping threats.  

- Implemented different enemy behaviors: periodic sound intervals for basic threats, a continuous chainsaw sound that masks other audio, and a “faker” that modifies pitch and hijacks the next phone call to create false feedback.  

- Built the UI around nine room buttons and a dedicated termination mode, where room buttons change color/state when a room is shut down, giving immediate visual feedback on player actions.  

- Centralized audio control in an `AudioManager`, allowing each room and enemy type to trigger sounds, adjust pitch and timing, and layer feedback without hardcoding logic into individual UI elements.

---
