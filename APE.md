[<--- Back to main Page](./index.md)
# A.P.E
A.P.E is a 2D sorting game built in C# with SFML, created as my first full game project at university. I focused on system architecture, card interaction logic, and the development of a reliable drag-and-drop framework for multiple item types. This project is significant because it demonstrates my early approach to structuring gameplay systems, solving UI/logic challenges, and organizing a multi-week development pipeline.

# Challenges
## Technical Challenges
- Designing a flexible state system (`TableManager`) that coordinates menu, dialogue, gameplay, and fail states.
- Implementing two different game modes (Category and List), each requiring unique evaluation logic while sharing core mechanics. 
- Building a dynamic container layout that adapts to different card types and container counts without breaking UI clarity.
- Creating a unified card architecture that supports four card types (Currency, Name, Crypto, Human) with shared behavior and custom logic.
- Parsing custom deck files with a JSON-like structure and interpreting them differently depending on the card type.
- Ensuring consistent drag-and-drop interaction across all card types using interface-driven design.

## Production & Workflow Challenges
- Finding the right balance between planning and execution during a multi-week project.
- Maintaining motivation when milestones were too large and provided no short-term feedback.
- Structuring development progress while managing university workload.