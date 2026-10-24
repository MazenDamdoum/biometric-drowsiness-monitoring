# Biometric Access and Drowsiness Monitoring

A low-cost access-control and driver-safety system that combines **fingerprint recognition**,
**facial recognition** and **drowsiness detection**. Built as a capstone design project (ELEC-4000,
University of Windsor, 2025).

## Results (measured on the hardware prototype)

| Module | Result | Time |
|---|---|---|
| Fingerprint recognition | 98.4% accuracy | 1.1 s |
| Facial recognition (ArcFace) | 95.6% accuracy | 0.95 s |
| Drowsiness detection (eye aspect ratio) | 90.3% sensitivity | 1.1 s |
| Multi-modal fusion | 99.2% accuracy | |

The hardware bill of materials came to **$355**, against about $2,200 for a comparable commercial
system (84% lower).

## How it works

- **Fingerprint:** enrols users and verifies them against templates stored in SQLite. Templates are
  XOR-encrypted (a demo scheme) and indexed by SHA-256 hash.
- **Face:** ArcFace-style embeddings, matched against enrolled users.
- **Drowsiness:** eye aspect ratio (EAR) tracked over time, raising an alert when the eyes stay closed
  past a threshold.
- **Fusion:** combines the fingerprint and face scores into one access decision. That cuts false
  accepts compared with either sensor alone.

[`biometric_system.py`](biometric_system.py) contains the full software stack, plus an interactive demo
menu: enrol, authenticate, monitor drowsiness, statistics and diagnostics. This version simulates the
sensor reads using the rates measured on the prototype, so it runs on any PC without the hardware.

## Run it

```bash
pip install -r requirements.txt
python biometric_system.py
```

## Stack

Python, OpenCV, NumPy, SQLite.
