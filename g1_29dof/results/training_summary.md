# G1 29DoF Training Summary

## Task

- Robot: Unitree G1 29DoF
- Task: Unitree-G1-29dof-Velocity
- RL framework: RSL-RL PPO
- Simulation: Isaac Lab / Isaac Sim
- Deployment target: MuJoCo sim2sim via unitree_rl_lab `g1_ctrl`

## Checkpoint Comparison

| Iteration | Mean Reward | Mean Episode Length | Terrain Level | XY Velocity Error | Yaw Velocity Error | Timeout Rate | Bad Orientation |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 5000 | 36.81 | 995.76 | 2.3832 | 0.3710 | 0.9658 | 0.9892 | 0.0108 |
| 8000 | 42.23 | 1000.00 | 4.7434 | 0.2912 | 0.7611 | 0.9977 | 0.0023 |
| 10000, after reward tuning | 42.65 | 1000.00 | 4.6413 | 0.3006 | 0.8413 | 0.9980 | 0.0017 |

## Reward / Metric Notes

### 5000 iterations

At 5000 iterations, the policy was already mostly stable, with a mean episode length of 995.76 and timeout rate of 0.9892. However, the terrain curriculum level was still relatively low at 2.3832, and the yaw velocity error was high at 0.9658.

Important metrics:

- `Mean reward`: 36.81
- `Mean episode length`: 995.76
- `track_lin_vel_xy`: 0.8544
- `track_ang_vel_z`: 0.2521
- `gait`: 0.5178
- `feet_slide`: -0.0469
- `joint_deviation_arms`: -0.0969
- `joint_deviation_legs`: -0.0936
- `error_vel_xy`: 0.3710
- `error_vel_yaw`: 0.9658

### 8000 iterations

At 8000 iterations, the mean reward increased to 42.23 and the mean episode length reached 1000.00, indicating that the robot was able to survive full episodes consistently. The terrain curriculum level increased to 4.7434, while both xy and yaw velocity errors decreased compared with the 5000-iteration checkpoint.

Important metrics:

- `Mean reward`: 42.23
- `Mean episode length`: 1000.00
- `track_lin_vel_xy`: 0.8989
- `track_ang_vel_z`: 0.2980
- `gait`: 0.4904
- `feet_slide`: -0.0303
- `joint_deviation_arms`: -0.0837
- `joint_deviation_legs`: -0.0821
- `error_vel_xy`: 0.2912
- `error_vel_yaw`: 0.7611

### 10000 iterations after reward tuning

After 8000 iterations, I adjusted several reward and penalty weights to reduce arm swinging and improve gait stability. The policy was then continued to 10000 iterations.

The final mean reward slightly increased to 42.65, and the episode length remained at 1000.00. The gait reward increased significantly from 0.4904 to 0.6877, suggesting improved gait regularity. The bad orientation termination rate also decreased from 0.0023 to 0.0017.

Important metrics:

- `Mean reward`: 42.65
- `Mean episode length`: 1000.00
- `track_lin_vel_xy`: 0.8940
- `track_ang_vel_z`: 0.2791
- `gait`: 0.6877
- `feet_slide`: -0.0360
- `joint_deviation_arms`: -0.1563
- `joint_deviation_legs`: -0.1010
- `error_vel_xy`: 0.3006
- `error_vel_yaw`: 0.8413

Note: Since reward weights were changed after 8000 iterations, individual reward terms after 10000 iterations are not directly comparable to earlier checkpoints. For example, more negative `joint_deviation_arms` or `joint_deviation_legs` can reflect stronger penalty weights rather than strictly worse behavior.

## Post-8000 Reward Tuning

After the 8000-iteration checkpoint, I tuned the reward weights with the following goals:

1. Reduce excessive arm swinging.
2. Improve gait regularity.
3. Reduce limping or asymmetric leg motion.
4. Improve stability during walking and turning.

The main tuning directions were:

- Increased `joint_deviation_arms` penalty to discourage excessive arm motion.
- Increased `gait` reward to encourage more regular stepping.
- Increased `feet_slide` penalty to reduce foot slipping.
- Slightly increased `action_rate` and `joint_acc` penalties to improve motion smoothness.
- Slightly increased `joint_deviation_legs` penalty to discourage abnormal leg poses.
- Increased or tested `track_ang_vel_z` weight to improve yaw tracking.

## Observations

From 5000 to 8000 iterations, the policy improved substantially in reward, terrain curriculum level, and velocity tracking. After reward tuning and continued training to 10000 iterations, the policy maintained full episode survival and showed improved gait reward, but yaw tracking still remained a weakness. In later sim2sim testing, right turns were mostly stable, while left turns sometimes introduced backward/rightward drift, suggesting that additional yaw-focused fine-tuning may be needed.
