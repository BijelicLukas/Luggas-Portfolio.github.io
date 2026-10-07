[<--- Back to main Page](./index.md)
# Possession
Possession is a two-week team project made in Unity with two other programmers. I built the enemy AI, a "Hunter" that patrols, chases, shoots and investigates, as a state machine in the first week. A teammate refined the AI further afterwards, and this page describes my original version.  

---

# Challenges

- Giving one enemy four clearly separated behaviors (patrolling, chasing, shooting, investigating) without ending up with one large update function full of nested conditions.  

- Defining when the enemy switches behavior: seeing the player long enough, being close enough to shoot, losing the player or noticing a clue.  

- Letting the enemy react to new clues while it is already investigating, without getting stuck on an old location.  

---

# Solutions

- Built the AI as a state machine with four state classes (`HunterPatrol`, `HunterHunt`, `HunterShoot`, `HunterInvestigation`). Each state owns its own behavior and only knows which transitions it may trigger.  

- Registered all allowed transitions up front through an `AddTransition` call per state, using a `Transition` enum. Illegal state changes are impossible by construction, and the whole behavior graph can be read in one place.  

  - **Patrol:** the Hunter walks between patrol points. If it sees the player long enough, it switches to Hunt.  

  - **Hunt:** the Hunter chases the player. Once close enough, it slows down and switches to Shoot.  

  - **Shoot:** the Hunter fires and reloads. It returns to Hunt if the player moves away, or to Investigation if the player is lost.  

  - **Investigation:** the Hunter checks the last known position or a clue. It can return to Hunt, fall back to Patrol, or restart Investigation at a new location when a new clue appears.  

- Gave every state the same lifecycle: `DoBeforeEntering` runs once when a transition into the state happens, `Act` handles the regular behavior every update, `Reason` decides what to do next and whether a transition is needed, and `DoBeforeLeaving` cleans up when the state is exited. Separating acting from reasoning kept each state's code short and made transitions easy to find.

---

<!-- # State Diagram
![Hunter state machine](./Assets/Possession_StateMachine.png)
*Four states and their transitions. [Add triggers, e.g. "sees player for X seconds", "distance < Y".]* -->

---

# Code Snippets

## State machine setup
```cs
HunterPatrol patrol = new(this);
HunterHunt hunt = new(this);
HunterShoot shoot = new(this);
HunterInvestigation investigation = new(this);

patrol.AddTransition(Transition.PatrolToHunt, hunt.ID);
patrol.AddTransition(Transition.PatrolToInvestigation, investigation.ID);

hunt.AddTransition(Transition.HuntToShoot, shoot.ID);

shoot.AddTransition(Transition.ShootToHunt, hunt.ID);
shoot.AddTransition(Transition.ShootToInvestigation, investigation.ID);

investigation.AddTransition(Transition.InvestigationToHunt, hunt.ID);
investigation.AddTransition(Transition.InvestigationToPatrol, patrol.ID);
investigation.AddTransition(Transition.InvestigationNewLocation, investigation.ID);
```
*All allowed transitions are declared in one place, so the full behavior graph is readable at a glance.*  

## HunterInvestigation (Week 1 version)
```cs
public class HunterInvestigation : State
{
    private float radius;
    private Vector3 lastSeenPlayerSpot;
    private float detectionRadius;
    private float dotThreshold;
    private HunterController controller;
    private float maxWaitingTime;
    //....

     public HunterInvestigation(HunterController controller) : base(controller)
    {
        stateID = StateID.HInvestigation;
        radius = controller.InvestigationRadius;
        lastSeenPlayerSpot = controller.lastSeenPlayer;
        detectionRadius = controller.InvestigationDetectionRadius;
        dotThreshold = controller.InvestigationDotFacingThreshold;
        maxWaitingTime = controller.InvestigationTime;
        //....
    }
}
```
*Week-one version: each state copies its tuning values from the controller. This was later replaced by a blackboard.*

---

# Lessons Learned

<!-- - [Your own point, e.g. what was easier or harder with a state machine than with if-chains.]  

- [Something about debugging transitions or tuning values like "seeing the player long enough".]   -->

- Working on AI in a team meant that a teammate later built on my code, which made clear structure and readable transitions important.

- In week one, every state read its settings (radius, speeds, thresholds) from a long list of variables on the `HunterController`. Between week one and week two we replaced this with a blackboard, which kept the controller small and let states share data without depending on the controller's internals.

- Splitting `Act` and `Reason` made it much easier to debug: when the enemy behaved wrong, I could tell right away whether the behavior or the decision to switch was at fault.