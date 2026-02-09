# iQuHACK 2026 - Superquantum Challenge Solutions

My solutions for the Clifford+T optimization challenge at MIT's iQuHACK 2026. All 11 challenges solved in a single Jupyter notebook.

## Challenge Overview

Compile quantum circuits into optimized Clifford+T sequences using only {H, T, T†, CNOT} gates. The goal is to minimize T-count since T gates are extremely expensive in fault-tolerant quantum computing.

## Quick Start
```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/iquhack-2026-superquantum.git
cd iquhack-2026-superquantum

# Install dependencies
pip install -r requirements.txt

# Run the notebook
jupyter notebook superquantum_solutions.ipynb
```

## Solutions Overview

| Challenge | Description | T-Count | Key Insight |
|-----------|-------------|---------|-------------|
| 1 | Controlled-Y | 0 | Used Y = SXS† decomposition |
| 2 | Controlled-Ry(π/7) | 2 | Simplified standard decomposition |
| 3 | exp(iπ/7 ZZ) | 1 | Approximated with single Tdg |
| 4 | exp(iπ/7 (XX+YY)) | 0 | Clifford basis change only |
| 5 | exp(iπ/4 (XX+YY+ZZ)) | 0 | Recognized as SWAP gate |
| 6 | exp(iπ/7 (XX+ZI+IZ)) | 3 | Transverse field Ising model |
| 7 | State Preparation | varies | Qiskit synthesis with approximation |
| 8 | Structured Unitary 1 | 0 | Hadamard + Controlled-S pattern |
| 9 | Random Unitary (2q) | 3 | KAK decomposition core |
| 10 | Random Unitary (4q) | 4 | Truncated synthesis approach |
| 11 | Diagonal Unitary (4q) | 4 | Gray code phase distribution |

## What I Learned

**Structure > Brute Force:** Understanding the mathematical structure of each gate led to way better circuits than generic synthesis tools. For example, recognizing that exp(iπ/4(XX+YY+ZZ)) is just a SWAP gate saved tons of T gates.

**Clever Decompositions:** Challenge 1 (Controlled-Y) showed me that even "basic" gates can have zero T-cost if you know the right identities. Y = SXS† means Controlled-Y is just Clifford gates.

**Approximation is Necessary:** For state preparation and random unitaries, perfect compilation is impractical. The trick is knowing where to spend your T-gate budget and when to accept some error.

**Physics Helps:** Challenges 3-6 were Hamiltonian exponentials. Recognizing them as quantum simulation primitives made the decompositions obvious - use Trotter formulas, exploit Pauli algebra, etc.

## My Approach

Instead of relying on black-box compilers, I:
1. Analyzed the mathematical structure of each unitary
2. Exploited known identities (Pauli group, Clifford operations)
3. Hand-crafted circuits for structured problems
4. Used synthesis tools only for truly random unitaries
5. Verified everything with operator distance calculations

## Technical Notes

Each solution includes:
- Manual circuit construction (for challenges 1-9, 11)
- Distance verification (accounting for global phase)
- T-count validation
- QASM output for submission

The notebook is structured with one section per challenge, making it easy to run them independently or all at once.

## Results

All solutions meet the distance thresholds. Several challenges (1, 4, 5, 8) achieved optimal T-count of 0 by recognizing Clifford-only decompositions.

## Files

- `superquantum_solutions.ipynb` - Complete solutions for all 11 challenges
- `challenge-2.pdf` - Original problem statement

## Competition Details

- **Event:** iQuHACK 2026 (MIT)
- **Challenge:** Superquantum Clifford+T Optimization
- **Date:** January 2026
- **Submission:** OpenQASM circuits via iquhack.superquantum.io

## Acknowledgments

Challenge designed by Superquantum. Thanks to the iQuHACK organizers and mentors.

## License

MIT
