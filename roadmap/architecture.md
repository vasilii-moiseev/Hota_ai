# Architecture Overview: Hota Bot Project

This document describes the architecture for the AI bot designed to play Heroes of Might and Magic 3: HOTA.

---

## High-Level Components

1. **Orchestrator**:
   - The central manager that initializes and coordinates all modules.
   - Ensures the workflow for processing game turns:
     1. AI Vision → Game State → Decision-Making → Action Execution.

2. **AI Vision Module**:
   - **Input**: Game screen (via screen capture).
   - **Output**: Processed data such as hero positions, resources, and enemy locations.
   - **Responsibilities**:
     - Capture and interpret game visuals.
     - Identify key elements on the screen.

3. **Game State Module**:
   - **Input**: Data from AI Vision.
   - **Output**: Current state of the game in a structured format.
   - **Responsibilities**:
     - Maintain an updated representation of the game environment.
     - Track elements like hero positions, resources, enemy units, and map layout.

4. **Decision-Making Module**:
   - **Input**: Current game state.
   - **Output**: Action (e.g., "move to (8,10)" or "engage in combat").
   - **Responsibilities**:
     - Determine optimal actions based on predefined rules or a reinforcement learning policy.
     - Use algorithms like heuristic evaluation, pathfinding, or neural networks.

5. **Action Execution Module**:
   - **Input**: Chosen action from Decision-Making.
   - **Output**: Simulated user input to the game (e.g., mouse clicks, keyboard actions).
   - **Responsibilities**:
     - Execute actions in the game environment.
     - Confirm successful execution and report back to the orchestrator.

---

## Data Flow

### **1. AI Vision → Game State**
- Captures the game screen and extracts structured data.
- Example Output: `{ "hero_position": (5,7), "resources": [(8,10)], "enemies": [(6,6)] }`

### **2. Game State → Decision-Making**
- Passes the current state to the decision-making engine.
- Example Input: `{ "hero_position": (5,7), "resources": [(8,10)], "enemies": [(6,6)] }`
- Example Output: `{"action": "move", "target": (8,10)}`

### **3. Decision-Making → Action Execution**
- Converts the chosen action into game interactions.
- Example: Simulate a mouse click on tile (8,10).

---

## Orchestrator Workflow

1. **Initialize Modules**:
   - Load AI Vision, Game State, Decision-Making, and Action Executor.

2. **Run Game Loop**:
   - Repeat the following until the game ends:
     1. AI Vision captures the game screen.
     2. Game State updates with the new data.
     3. Decision-Making selects the next action.
     4. Action Execution performs the action.

---

## Future Enhancements
1. **Reinforcement Learning**:
   - Replace rule-based decision-making with a policy trained using RL.
2. **Error Handling**:
   - Improve robustness to handle unexpected game scenarios or module failures.

---

