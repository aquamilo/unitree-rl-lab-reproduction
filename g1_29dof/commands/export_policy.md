# Export Policy from RSL-RL Checkpoint

```bash
cd ~/l_lab/unitree_rl_lab

CKPT=$(find logs/rsl_rl -name "model_9999.pt" | sort -V | tail -n 1)
RUN_DIR=$(dirname "$CKPT")
RUN_NAME=$(basename "$RUN_DIR")

python scripts/rsl_rl/play.py \
  --headless \
  --task Unitree-G1-29dof-Velocity \
  --load_run "$RUN_NAME" \
  --checkpoint "$CKPT" \
  --num_envs 1
```

Exported ONNX will be at:

```
$RUN_DIR/exported/policy.onnx
```
