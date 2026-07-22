# Fourier and Gate-Redundancy Analysis of Data-Reuploading Quantum Circuits

## Research question

**When does another data-reuploading layer create genuinely new input dependence, and when can its gates be simplified without changing the model's function family?**

A variational quantum model produces an expectation value

\[
f_\theta(x)=\langle 0|U^\dagger(x,\theta)\,Z\,U(x,\theta)|0\rangle.
\]

For common data-encoding circuits, this output can be written as a finite Fourier series in \(x\). This project studies how rotation-axis choice, noncommutativity, measurement, and trainable parameters determine:

- accessible Fourier frequencies;
- active versus suppressed Fourier coefficients;
- redundant gates and parameters;
- minimal circuits representing the same function family.

## First milestone

The notebook symbolically analyzes four one-qubit circuits:

1. \(R_Y(x)\)
2. \(R_Y(\theta)R_Y(x)\)
3. \(R_Y(x)R_Z(\theta)R_Y(x)\)
4. \(R_Y(x)R_X(\theta)R_Y(x)\)

It derives their exact \(Z\)-expectation values, extracts Fourier coefficients, and checks whether extra gates add a new frequency or merely change an existing coefficient.

## Preliminary observations

- Same-axis rotations combine: \(R_Y(a)R_Y(b)=R_Y(a+b)\).
- A trainable same-axis gate can change phase without expanding the frequency set.
- Re-uploading separated by a noncommuting rotation can produce a second harmonic.
- A frequency may be allowed by the architecture but disappear for special parameter values.

## Planned extension

1. Enumerate short circuits made from \(R_X,R_Y,R_Z\).
2. Symbolically derive \(f_\theta(x)\).
3. Group circuits with identical output-function families.
4. Find minimal representatives.
5. Extend from one feature to two features and from one qubit to two qubits.
6. Use simulation only to validate the symbolic results and later study noise.

## Why this matters

Gate count alone does not measure useful model capacity. A larger circuit may contain gates that are algebraically mergeable, invisible under the chosen measurement, or unable to activate new Fourier components. Finding smaller equivalent circuits can reduce depth and noise while preserving expressive power.

## Run locally

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

pip install -r requirements.txt
jupyter notebook Fourier_Gate_Redundancy.ipynb
```

## References

- A. Pérez-Salinas et al., *Data re-uploading for a universal quantum classifier*, Quantum 4, 226 (2020), arXiv:1907.02085.
- M. Schuld, R. Sweke, and J. J. Meyer, *The effect of data encoding on the expressive power of variational quantum machine learning models*, Physical Review A 103, 032430 (2021), arXiv:2008.08605.
- PennyLane documentation: `qml.fourier`.
