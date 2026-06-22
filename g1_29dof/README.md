# Unitree G1 29DoF Sim2Sim Deployment

This folder documents my Unitree G1 29DoF velocity policy training and MuJoCo sim2sim deployment workflow.

## What I Did

- Trained a G1 29DoF velocity policy using RSL-RL.
- Exported `model_9999.pt` to `policy.onnx`.
- Integrated `policy.onnx` into the `g1_ctrl` C++ deploy pipeline.
- Modified FSM transition logic to support keyboard control:
  - `f`: Passive -> FixStand
  - `v`: FixStand -> Velocity
  - `p`: return to Passive
- Modified velocity command input to use keyboard commands:
  - `w`: forward
  - `s`: backward
  - `a`: left
  - `d`: right
  - `q`: turn left
  - `e`: turn right

## Model Files

- `models/model_4999.pt`: RSL-RL checkpoint 1
- `models/model_7999.pt`: RSL-RL chechpoint 2
- `models/model_9999.pt`: RSL-RL final checkpoint
- `models/policy.onnx`: exported ONNX policy for deployment

## Sim2Sim Startup

See `commands/run_mujoco.md` and `commands/run_g1_ctrl.md`.
