# Exp No: 10 – Implementation of Classical Planning Algorithm

### Name: Navaneeth S
### Register Number:212225240097
---

# Aim

To study and implement the **Classical Planning Algorithm** for generating a sequence of actions that transforms an **initial state** into a **goal state**.

---

# Problem Description

Classical Planning is an important concept in **Artificial Intelligence** that deals with finding a sequence of actions to achieve a specified goal from a given initial state. A planning agent uses knowledge about the environment, available actions, their preconditions, and effects to determine an appropriate plan.

Each action consists of:

- **Precondition:** The conditions that must be satisfied before an action can be performed.
- **Effect:** The changes made to the current state after the action is executed.

The planning process repeatedly selects applicable actions until the goal state is achieved.

---

# Algorithm

1. Define the initial state.
2. Define the goal state.
3. Define the available actions along with their preconditions and effects.
4. Compare the current state with the goal state.
5. Identify the actions whose preconditions are satisfied.
6. Apply the effects of the selected action to generate a new state.
7. Continue applying valid actions until the goal state is reached.
8. Store the executed actions in order to form the plan.
9. Display the final sequence of actions.

---

# Example 1

### Initial State

```text
A → Table
B → Table
```

### Goal State

```text
A → B
B → Table
```

### Plan Generated

```text
move_A_to_B
```

---

# Example 2

### Initial State

```text
A → Table
B → Table
C → Table
```

### Goal State

```text
A → B
B → C
C → Table
```

### Plan Generated

```text
move_A_to_B
move_B_to_C
```

---

# Working Principle

- The planner begins with the initial state.
- It checks whether the current state satisfies the goal state.
- If the goal is not achieved, it searches for actions whose preconditions are true.
- The selected action is executed, and its effects modify the current state.
- The process continues until the goal state is reached.
- The ordered list of executed actions forms the final plan.

---

# Advantages

- Produces an optimal sequence of actions for simple planning problems.
- Demonstrates logical reasoning and decision-making.
- Can be applied to automated planning and scheduling tasks.
- Forms the basis for many AI planning systems.

---

# Applications

- Robotics
- Automated planning systems
- Intelligent scheduling
- Navigation systems
- Game AI
- Logistics and resource management

---
# PROGRAM:
```
from collections import deque

def satisfies(state, condition):
    for key, value in condition.items():
        if state.get(key) != value:
            return False
    return True

def apply_action(state, effect):
    new_state = state.copy()
    new_state.update(effect)
    return new_state

def find_plan(initial_state, goal_state, actions):
    queue = deque()
    queue.append((initial_state, []))
    visited = set()

    while queue:
        current_state, plan = queue.popleft()

        state_key = tuple(sorted(current_state.items()))

        if state_key in visited:
            continue

        visited.add(state_key)

        # Goal Test
        if satisfies(current_state, goal_state):
            return plan

        # Expand all applicable actions
        for action_name, action in actions.items():
            if satisfies(current_state, action["precondition"]):
                next_state = apply_action(current_state, action["effect"])
                queue.append((next_state, plan + [action_name]))

    return None


print("Example 1")

initial_state = {
    'A': 'Table',
    'B': 'Table'
}

goal_state = {
    'A': 'B',
    'B': 'Table'
}

actions = {
    'move_A_to_B': {
        'precondition': {
            'A': 'Table',
            'B': 'Table'
        },
        'effect': {
            'A': 'B'
        }
    },

    'move_B_to_Table': {
        'precondition': {
            'A': 'Table',
            'B': 'B'
        },
        'effect': {
            'B': 'Table'
        }
    }
}

plan = find_plan(initial_state, goal_state, actions)

print("Plan:", plan)


print("\nExample 2")

initial_state = {
    'A': 'Table',
    'B': 'Table',
    'C': 'Table'
}

goal_state = {
    'A': 'B',
    'B': 'C',
    'C': 'Table'
}

actions = {
    'move_A_to_B': {
        'precondition': {
            'A': 'Table',
            'B': 'Table'
        },
        'effect': {
            'A': 'B'
        }
    },

    'move_B_to_C': {
        'precondition': {
            'A': 'B',
            'B': 'Table',
            'C': 'Table'
        },
        'effect': {
            'B': 'C'
        }
    },

    'move_C_to_Table': {
        'precondition': {
            'A': 'B',
            'B': 'C',
            'C': 'C'
        },
        'effect': {
            'C': 'Table'
        }
    }
}

plan = find_plan(initial_state, goal_state, actions)

print("Plan:", plan)
```
# OUTPUT:
<img width="335" height="104" alt="image" src="https://github.com/user-attachments/assets/5da82a34-9a1f-4d3b-82af-3283eaf8c8a7" />

# Result

Thus, the **Classical Planning Algorithm** was successfully studied and implemented to generate a valid sequence of actions that transforms the initial state into the desired goal state.
