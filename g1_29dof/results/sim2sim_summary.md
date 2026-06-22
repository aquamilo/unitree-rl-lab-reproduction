# G1 29DoF Sim2Sim Summary

## Completed

- Built and ran `unitree_mujoco`.
- Built and ran `g1_ctrl`.
- Fixed missing shared library issues for `libddsc.so` and ONNX Runtime.
- Connected `g1_ctrl` to MuJoCo using DDS over network interface `wlp131s0`.
- Exported trained RSL-RL checkpoint to ONNX.
- Modified FSM transition logic for keyboard-based control.
- Modified deploy observation input from `velocity_commands` to `keyboard_velocity_commands`.
- Verified G1 standing and velocity policy execution in MuJoCo.

## Known Issues

- Keyboard repeat may be affected by remote desktop software such as ToDesk.
- Left turning may produce backward/right drift and may require further yaw-focused fine-tuning.
- Real robot deployment has not been included in this public repository.
