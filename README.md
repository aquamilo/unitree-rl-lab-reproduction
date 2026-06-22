# Unitree RL Lab Reproduction and Sim2Sim Deployment

This repository documents my reproduction and extension work on Unitree robot reinforcement learning using Isaac Lab, Unitree RL Lab, and MuJoCo sim2sim.

## Highlights

- Trained and evaluated Unitree G1 29DoF velocity policies.
- Exported RSL-RL checkpoints to ONNX.
- Integrated the exported policy into the Unitree RL Lab C++ deploy pipeline.
- Debugged DDS communication between `unitree_mujoco` and `g1_ctrl`.
- Added keyboard-based FSM transitions for no-joystick sim2sim control.
- Added keyboard velocity commands for `w/s/a/d/q/e` control.
- Verified the policy in MuJoCo sim2sim.

## Repository Structure

```text
g1_29dof/
├── commands/      # commands for running MuJoCo, controller, and export
├── configs/       # modified config files
├── patches/       # code changes and patch files
├── models/        # model9999.pt and policy.onnx
└── results/       # training and sim2sim notes
```

## Notes

This repository only contains my reproduction notes, modified configuration files, patches, and small exported model files. It does not include the full upstream repositories, Isaac Sim installation files, Unitree model assets, or private robot/network configuration.

## Upstream Projects

- `unitree_rl_lab`
- `unitree_mujoco`
- `Isaac Lab`
- `RSL-RL`
