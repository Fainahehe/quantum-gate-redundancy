# Fourier and Gate-Redundancy Analysis of Data-Reuploading Quantum Circuits

## Project overview

This project studies a question that is more specific than simply comparing model accuracy:

> **When does an additional data-reuploading layer create genuinely new mathematical behaviour, and when is it redundant?**

A variational quantum circuit produces an expectation value of the form

$$
f_{\theta}(x)
=
\langle 0|
U^{\dagger}(x,\theta)\,
Z\,
U(x,\theta)
|0\rangle.
$$

For many data-encoding circuits, this output can be written as a finite Fourier series in the input $x$.

The project investigates how the following affect the represented function:

- rotation-axis choice;
- noncommuting gates;
- repeated data encoding;
- trainable parameters;
- measurement choice;
- gate redundancy.

---

## Main research questions

1. Which gate sequences introduce new Fourier frequencies?
2. Which additional gates only modify existing coefficients?
3. When can a larger circuit be replaced by a smaller equivalent circuit?
4. Can two circuits have the same accessible frequencies but different function families?
5. Which parameter values suppress otherwise accessible frequencies?

---

## Circuits analyzed

The starter notebook symbolically analyzes four one-qubit circuits:

1. $R_Y(x)$
2. $R_Y(\theta)R_Y(x)$
3. $R_Y(x)R_Z(\theta)R_Y(x)$
4. $R_Y(x)R_X(\theta)R_Y(x)$

For each circuit, the notebook:

- constructs the unitary matrix;
- applies it to $|0\rangle$;
- calculates the exact $Z$-expectation value;
- extracts its Fourier coefficients;
- identifies accessible frequencies;
- checks for algebraic simplifications;
- verifies the symbolic result numerically.

---

## Initial results

### Circuit 1: one upload

$$
U_1(x)=R_Y(x)
$$

The output is

$$
f_1(x)=\langle Z\rangle=\cos(x).
$$

Its complex Fourier frequency set is

$$
\Omega_1=\{-1,1\}.
$$

---

### Circuit 2: same-axis trainable rotation

$$
U_2(x,\theta)=R_Y(\theta)R_Y(x).
$$

Rotations around the same axis combine:

$$
R_Y(\theta)R_Y(x)=R_Y(x+\theta).
$$

Therefore,

$$
f_2(x,\theta)=\cos(x+\theta).
$$

The parameter changes the Fourier coefficients, but it does not add a new frequency.

---

### Circuit 3: re-uploading with an $R_Z$ separator

$$
U_3(x,\theta)=R_Y(x)R_Z(\theta)R_Y(x).
$$

The exact output is

$$
f_3(x,\theta)
=
\sin^2\left(\frac{\theta}{2}\right)
+
\cos^2\left(\frac{\theta}{2}\right)\cos(2x).
$$

The accessible frequencies are

$$
\Omega_3=\{-2,0,2\}.
$$

The second harmonic is parameter dependent. For example:

- when $\theta=0$, the output contains $\cos(2x)$;
- when $\theta=\pi$, the second harmonic disappears.

---

### Circuit 4: re-uploading with an $R_X$ separator

$$
U_4(x,\theta)=R_Y(x)R_X(\theta)R_Y(x).
$$

The output is

$$
f_4(x,\theta)
=
-\sin^2\left(\frac{\theta}{2}\right)
+
\cos^2\left(\frac{\theta}{2}\right)\cos(2x).
$$

This circuit has the same accessible frequency set as Circuit 3,

$$
\Omega_4=\{-2,0,2\},
$$

but different Fourier coefficients.

This shows that identical frequency sets do not necessarily imply identical parameterized function families.

---

## Preliminary catalogue

| Circuit | Exact output | Frequencies | Main observation |
|---|---|---|---|
| $R_Y(x)$ | $\cos(x)$ | $\{-1,1\}$ | One upload |
| $R_Y(\theta)R_Y(x)$ | $\cos(x+\theta)$ | $\{-1,1\}$ | Gates combine exactly |
| $R_Y(x)R_Z(\theta)R_Y(x)$ | $\sin^2(\theta/2)+\cos^2(\theta/2)\cos(2x)$ | $\{-2,0,2\}$ | Adds a second harmonic |
| $R_Y(x)R_X(\theta)R_Y(x)$ | $-\sin^2(\theta/2)+\cos^2(\theta/2)\cos(2x)$ | $\{-2,0,2\}$ | Same spectrum, different coefficients |

---

## Types of redundancy

The project distinguishes three different ideas.

### 1. Unitary redundancy

Two circuits implement the same unitary, possibly up to global phase.

### 2. Measurement redundancy

Two circuits implement different unitaries but produce the same chosen expectation value.

### 3. Function-family redundancy

Two parameterized circuits generate the same set of functions as their parameters vary.

These three forms of equivalence are not the same.

---

## Why this matters

Gate count alone does not measure useful model capacity.

A larger circuit may contain gates that are:

- algebraically mergeable;
- invisible under the selected measurement;
- unable to activate new Fourier components;
- redundant for the represented function family.

Finding smaller equivalent circuits may reduce:

- circuit depth;
- hardware noise;
- training cost;
- unnecessary parameters.

The goal is therefore not simply to build a more expressive circuit, but to find the **smallest circuit that produces the desired mathematical behaviour**.

---

## Planned extensions

1. Enumerate short circuits built from $R_X$, $R_Y$, and $R_Z$.
2. Symbolically derive $f_{\theta}(x)$ for each architecture.
3. Extract and compare Fourier coefficients.
4. Detect adjacent same-axis rotations.
5. Identify parameter values that suppress frequencies.
6. Group circuits into equivalent function families.
7. Find minimal representatives.
8. Extend from one input feature to two.
9. Extend from one qubit to two qubits.
10. Study the effect of entangling gates and measurement choice.

---

## Repository contents

```text
quantum-gate-redundancy/
├── Fourier_Gate_Redundancy.ipynb
├── PROJECT_BRIEF.md
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Run the notebook locally

### 1. Create a virtual environment

```bash
python -m venv .venv
```

### 2. Activate it

Windows:

```powershell
.venv\Scripts\activate
```

macOS or Linux:

```bash
source .venv/bin/activate
```

### 3. Install the dependencies

```bash
pip install -r requirements.txt
```

### 4. Open the notebook

```bash
jupyter notebook Fourier_Gate_Redundancy.ipynb
```

---

## Possible contribution

A realistic contribution from this project could be:

- a catalogue of minimal one-qubit re-uploading circuits;
- a proof about which separators activate particular Fourier coefficients;
- a counterexample showing that equal spectra do not imply equal function families;
- a symbolic program that detects redundant gates and parameters;
- a design rule for producing a chosen harmonic with the fewest gates.

---

## References

1. A. Pérez-Salinas, A. Cervera-Lierta, E. Gil-Fuster, and J. I. Latorre, *Data re-uploading for a universal quantum classifier*, Quantum 4, 226 (2020), arXiv:1907.02085.
2. M. Schuld, R. Sweke, and J. J. Meyer, *The effect of data encoding on the expressive power of variational quantum machine learning models*, Physical Review A 103, 032430 (2021), arXiv:2008.08605.
3. PennyLane documentation, `qml.fourier`.
