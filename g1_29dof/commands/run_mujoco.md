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


# Run MuJoCo G1 Simulation

```bash
cd ~/l_lab/unitree_mujoco/simulate/build
./unitree_mujoco -i 0 -n <your_interface_name> -r g1 -s scene.xml
```

Alternative 29DoF flat scene:

```bash
cd ~/l_lab/unitree_mujoco/simulate/build
./unitree_mujoco -i 0 -n <your_interface_name> -r g1 -s scene_29dof.xml
```
