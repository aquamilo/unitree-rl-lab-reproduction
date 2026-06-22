## Network Interface Note

The network interface name is not fixed and may differ across machines.

For example, it may be:
- wlp131s0 (WiFi)
- wlan0
- wlo1
- enp3s0 (wired Ethernet)

### How to find your interface name

You can check your active network interface using:

```bash
ip link show
```

or:

```bash
nmcli device status
```

Look for the interface with:
- TYPE = wifi (or ethernet)
- STATE = connected

The correct interface is the one currently connected to the network.
Tip: If the network interface is incorrect, DDS communication between MuJoCo and g1_ctrl will fail.


# Run G1 Controller

```bash
cd ~/l_lab/unitree_rl_lab/deploy/robots/g1_29dof/build

export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib:$HOME/l_lab/unitree_rl_lab/deploy/thirdparty/onnxruntime-linux-x64-1.22.0/lib

./g1_ctrl --network <your_interface_name>
```

## Keyboard Control

### FSM transitions
- f: Passive -> FixStand
- v: FixStand -> Velocity
- p: Return to Passive

### Velocity commands
- w: forward
- s: backward
- a: move left
- d: move right
- q: turn left
- e: turn right

## Startup Sequence
1. Start MuJoCo
2. Start g1_ctrl
3. Focus g1_ctrl terminal → press `f`
4. Focus MuJoCo → press `8`
5. Back to g1_ctrl → press `v`
6. MuJoCo → press `9`
7. Control with w/s/a/d/q/e
