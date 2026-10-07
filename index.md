# Lukas Bijelic
Game Development student at FH Salzburg, focused on gameplay systems, architecture and algorithms.  
This site shows how I work: technical notes, design decisions, problems I ran into, and what I would do differently today.

# Projects

## [Possession](Possession.md)
A two-week Unity team project with two other programmers. I built the enemy AI in the first week.  
**Systems:** a state-machine-based enemy AI with four states (Patrol, Hunt, Shoot, Investigation) and explicitly declared transitions. Each state follows the same lifecycle (`DoBeforeEntering`, `Act`, `Reason`, `DoBeforeLeaving`).

---

## [Last Response](./Last_Response.md)
A solo GameJam project made in **Unity** (theme: *Lost Signal*): 
monitor nine rooms by phone and decide which ones need to be shut down.  
**Systems:** an event-based room system that keeps room logic and enemy behaviors decoupled, with a shared ScriptableObject as the single source of truth for room data.   
*Itch.io Page:* [Last Response Game-Page](https://lugas-games.itch.io/last-response)

---

## [A.P.E - Automated Productivity Evaluation](./APE.md)
A 2D sorting game built in **C# with SFML**, my first full game project.  
**Systems:** a layered card architecture (abstract base class, two game-mode types, four concrete card types), a unified drag-and-drop framework built on an `IDraggable` interface, and data-driven levels defined in custom deck files.  
*Itch.io Page:* [A.P.E Game-Page](https://lugas-games.itch.io/ape)

---

<!-- ## [Duck You](./DuckYou.md)
A **GameJam project** made during one of my first weeks in school.  
Theme: *Tension*  
Our idea was a 4-player couch-co-op "subway surfer".  
I implemented controller support for four players simultaneously - something completely new for me at the time.  
(There is no Itch.io page for this one)  

---

## [Spider MOMmy](./SpiderMommy.md)
A **Gamejam project** developed with a small first-semester team.  
Theme: *No strings attached*  
The gamplay is split between two players:  
a first-person adventurer and a top-down spider protecting them.  
My role focused on enemy behaviour, but I also supported team members with general Unity systems and logic.  
*Itch.io Page:* [Spider MOMmy Game Page](https://prehnit.itch.io/spider-mommy) -->

