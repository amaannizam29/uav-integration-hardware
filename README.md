# UAV Integration Hardware

Custom-designed mechanical components for integrating avionics and power onto a VTOL UAV airframe. Each part solves a specific integration problem on an existing platform, designed in Fusion 360.

This is a growing collection. Parts are added as they are designed; each gets its own entry below and its files under `parts/`.

Scope: integration and modification hardware, not airframe design. The airframe is an existing platform; these parts adapt avionics and power to it.

Related work:

- TriFlight Avionics Research — the avionics/systems research foundation
- UAV Failure Detection — the ML failure-detection extension

## Parts index

| Part | Purpose | Status |
|---|---|---|
| Battery lock tray | CG-stable battery retention through VTOL transition | Complete |
| Lift-motor mount | Holds a lift motor on a carbon boom, vibration-aware | Complete |
| FC tray | Vibration-isolated flight-controller mount | Complete |
| (next part) | (purpose) | Planned |

## Parts

### 1. Battery lock tray (BATT_LOCK_TRAY_V1)

**Problem.** During VTOL transition the airframe sees combined vertical (lift) and forward (pusher) accelerations plus vibration. A battery held only by velcro can shift, moving the center of gravity during the most control-critical phase of flight.

**Solution.** A slide-in tray with a cam-lock. The battery slides in leads-first; a pivoting cam at the rear rotates down and its off-center head physically blocks the battery from sliding out, positive mechanical retention, not friction.

**Key features.**

- Cam-lock at the rear for positive retention
- Wire-exit notch at the opposite end so the lock never pinches the leads
- Strain-relief slot near the wire end (zip-tie anchor)
- Mounting tabs with M3 holes to bolt to the airframe

Files: `parts/battery_lock_tray/`

### 2. Lift-motor mount (LIFT_MOTOR_MOUNT_V1)

**Problem.** A QuadPlane conversion needs vertical lift motors held out on carbon booms. The mount must carry motor thrust and the vibration lift motors produce during hover, the same vibration that, uncontrolled, corrupts IMU data.

**Solution.** A bracket with a motor mount plate on top, a structural spine, and a split clamp that grips the carbon boom and tightens with two bolts.

**Key features.**

- Motor bolt pattern on the top plate + center pass-through for phase wires
- Split clamp around the boom tube, adjustable position along the boom
- Two M3 clamp bolts to lock onto the tube
- Structural spine sized for thrust and vibration loads

Files: `parts/lift_motor_mount/`

### 3. Flight controller tray (FC_TRAY_V1)

**Problem.** The flight controller's IMU is highly sensitive to vibration. Airframe and motor vibration, especially the lift-motor vibration during hover, feeds straight into the accelerometers and gyros and corrupts the attitude estimate. A rigidly bolted FC reads that noise directly. It is the same vibration signature that, in the failure-detection work, indicates a motor problem, here the goal is to keep it out of the flight controller.

**Solution.** A two-level tray. A base bolts to the airframe; the FC platform floats above it on four anti-vibration grommets. The grommets damp vibration between the airframe and the board before it reaches the IMU.

**Key features.**

- FC platform isolated from the base on four soft grommet mounts (grommet pockets)
- Standard 30.5mm FC bolt pattern, fits common flight controllers
- Airframe mounting holes in the base (M3)
- Wire/USB notch in the platform edge for cable access

Files: `parts/fc_tray/`

## Repository structure

```
uav-integration-hardware/
├── README.md
└── parts/
    ├── battery_lock_tray/
    │   ├── *.step        (universal CAD, opens in any CAD tool)
    │   ├── *.f3d         (Fusion 360 native, optional)
    │   └── *.png         (render / screenshot)
    ├── lift_motor_mount/
    │   ├── *.step
    │   ├── *.f3d
    │   └── *.png
    └── fc_tray/
        ├── *.step
        ├── *.f3d
        └── *.png
```

Each part folder holds: a STEP file (universal, viewable by anyone), optionally the Fusion native file, and at least one image so the part is visible on GitHub without opening CAD.

## File formats

- **STEP (.step / .stp):** universal CAD exchange format. Anyone can open it in any CAD tool. This is the format to always include.
- **Fusion (.f3d):** native Fusion 360 file with full design history. Optional, for editing in Fusion.
- **PNG:** a render or screenshot so the part shows on GitHub without CAD software.

## Design notes

- All fasteners are M3 unless noted.
- Dimensions are sized to standard parts (6S battery, 16mm carbon boom, common lift-motor bolt patterns, 30.5mm FC mounting pattern) and should be verified against the actual hardware before printing or manufacture.
- Intended for 3D printing in PETG or Nylon for structural parts.

## Honest scope

These are integration components designed to demonstrate mechanical-design capability and solve real VTOL integration problems. They are not a complete aircraft, and dimensions are design intents pending verification against final hardware.
