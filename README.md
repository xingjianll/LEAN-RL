# LEAN-RL

Train LLM to produce Lean 4 code using inverse reinforcement learning.

## Approach

Lean 4 proofs are modeled as Markov processes:
- **State**: Current proof state (goals + hypotheses)
- **Action**: Tactic application
- **Reward**: Learned from expert proofs via inverse RL
- **Terminal**: All goals closed

## Architecture

```
LEAN-RL/
├── data/           # Expert proofs (mathlib, LeanDojo)
├── src/            # Core implementation
│   ├── environment/    # Lean 4 proof environment
│   ├── reward/         # Reward learning (GAIL, AIRL, etc.)
│   └── policy/         # LLM policy for tactic selection
└── experiments/    # Training scripts
```

## Usage

```python
from lean_rl.environment import LeanEnvironment
from lean_rl.reward import InverseRLLearner
from lean_rl.policy import LLMStrategy

# Load expert proofs
env = LeanEnvironment()
expert_data = env.load_expert_proofs("mathlib")

# Learn reward function
reward_learner = InverseRLLearner(expert_data)
reward_fn = reward_learner.learn()

# Train policy
policy = LLMStrategy(reward_fn)
policy.train()
```
