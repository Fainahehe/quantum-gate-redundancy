# Mini-Project Proposal

## Fourier and Gate-Redundancy Analysis of Data-Reuploading Quantum Circuits

**Objective.** Determine when repeated data encoding gives a variational quantum model genuinely new functional capacity and when additional gates are redundant.

**Motivation.** Quantum-circuit efficiency is often summarized using gate count or depth, but these measures do not reveal whether every gate changes the represented function. In data-reuploading models, repeated encoding can enlarge the Fourier spectrum of the model output. However, same-axis rotations may combine, some gates may be invisible under a selected measurement, and trainable parameters can suppress theoretically accessible frequencies.

**Method.** Begin with one-qubit circuits containing \(R_X\), \(R_Y\), and \(R_Z\) gates. Symbolically derive the expectation value \(f_\theta(x)=\langle Z\rangle\), extract its Fourier coefficients, and classify circuits by accessible frequencies and represented function families. Develop automated checks for three kinds of redundancy: unitary equivalence, measurement equivalence, and function-family equivalence. Validate symbolic results numerically and later extend the analysis to two features and two qubits.

**Initial result.** \(R_Y(\theta)R_Y(x)\) simplifies to \(R_Y(x+\theta)\), so it does not expand the frequency set. In contrast, \(R_Y(x)R_Z(\theta)R_Y(x)\) can produce a constant term and a second harmonic \(\cos(2x)\), although the harmonic disappears for particular parameter values.

**Potential contribution.** A catalogue or software tool identifying minimal circuits capable of producing chosen Fourier spectra, together with mathematical design rules explaining when noncommuting separators add useful capacity per gate.
