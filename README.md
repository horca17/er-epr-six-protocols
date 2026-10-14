# Six Quantum Hardware Protocols Testing Boundary Signatures of the ER=EPR Conjecture

Code and data for the paper by **Horacio S. Cáceres** (independent researcher, Córdoba, Argentina). Version 3, 14 October 2026 (v2: 12 October 2026; v1: 5 June 2026).
DOI (all versions): [10.5281/zenodo.20559368](https://doi.org/10.5281/zenodo.20559368) · v3: [10.5281/zenodo.23376704](https://doi.org/10.5281/zenodo.23376704) · v2: [10.5281/zenodo.23321402](https://doi.org/10.5281/zenodo.23321402)

These are six quantum-circuit experiments run on **ibm_marrakesh** (IBM Quantum, 156 qubits, Heron R2), April–May 2026, using 7 min 02 s of QPU time in total.

## Scope

The experiments run entirely on the **boundary (CFT) side**. They implement information dynamics in quantum circuits, not bulk spacetime geometry.

- **Measured on hardware:** the numbers in the table below.
- **Interpretation:** the reading of these numbers as signatures of ER=EPR, within the AdS₂/JT gravity framework with SYK as the boundary dual. This is an interpretation, not a measurement.

## Results and IBM Quantum jobs

Every job can be retrieved with `QiskitRuntimeService().job("<job_id>")`, so anyone can check the raw results.

| # | Experiment | Main result | Job ID | QPU time |
|---|---|---|---|---|
| 1 | GHZ state, Mermin operator | \|⟨M⟩\| = 3.885 (classical bound 2, quantum max 4) | `d7g38hma0v2s738abtf0` (Estimator) · `d7g38hua0v2s738abtg0` (Sampler) | 34 s + 7 s |
| 2 | GJW traversable wormhole, Bell-pair TFD | F(g=π/2) = 1.01 ± 0.01 | `d7gft2jjne2c7392r44g` | 21 s |
| 3 | Hayden–Preskill with SYK scrambler | F_scr = 0.530 (sim 0.532) | `d7gls13jne2c73932620` | 18 s |
| 2b | GJW with SYK scrambling and Majorana coupling | F(g=0) = 0.020 · F(g=π/2) = 0.953 · gain 0.933 | `d7h873q2khts739peivg` | 50 s |
| 5 | OTOCs, Lyapunov exponent | λ_L = 1.975 ± 0.294 (54.8 % of the MSS bound) | `d7jaamkolufs73etbrfg` | 25 s |
| 6 | Black hole entropy under absorption (Bekenstein) | Energy response ⟨H_SYK⟩: corr. 0.998 with simulation. Entropy: S(t) growth reproduced over a ≈0.3-bit noise floor; area growth ΔA(θ) **not resolved on hardware** (simulation: 0.348 → 0.496 / 0.635 bits) | `d7t6lj7ljm6s73bc82c0` | 4 min 27 s |

**Version 3** corrects Experiments 2 and 3: Exp. 2 reports the raw F(g=π/2) = 1.01 ± 0.01 instead of the clipped 1.000; in Exp. 3 the fused U†U circuit (F = 0.9983) is a noise-floor control, not hardware recovery (hardware scrambling F_scr = 0.530 vs. 0.532 in simulation; recovery shown in simulation).

**Version 2** corrects Experiment 6: version 1 reported the simulated entropy values as hardware results.

The numbering follows the order of execution. Exp 2b came after Exp 3, once the limits of the Bell-pair approximation were clear.

## Repository layout

```
notebooks/   one notebook per experiment (exp1_…, exp2_…, exp3_…, exp2b_…, exp5_…, exp6_…)
reproduce/   short notebooks that download each IBM job and recompute the numbers in the paper
paper/       the PDF (same file as on Zenodo)
```

## Reproduce

- Quickest check: run the notebooks in `reproduce/`. Each one retrieves the job by its ID (needs an IBM Quantum account), recomputes the result and prints it next to the paper value.
- Requirements: Python 3.10+, `qiskit` 2.x, `qiskit-ibm-runtime`, `numpy`, `scipy`, `matplotlib`. Every notebook runs on `AerSimulator` without an IBM account.
- IBM credentials: save them once with `QiskitRuntimeService.save_account(...)` on your own machine. **Never put them inside a notebook.**
- Observables on transpiled circuits: map them to the physical layout with `obs.apply_layout(qc_t.layout)`.
- Mermin operator: `SparsePauliOp(["XYY","YXY","YYX","XXX"], coeffs=[-1,-1,-1,1])`, which is the paper's M with the opposite overall sign, so the ideal GHZ state gives +4. The paper reports |⟨M⟩|.

## Verify the paper

```
sha256: 7cd9e67a0b6e3116d6dc8cd0751d2318c8061893ce1ed65c9151ce3ffd99fb67  paper/er-epr-six-protocols-2026-v3.pdf  (v3)
sha256: 977f89706666ecd25278b8815698e2727bc3df6361585b4902ee67d291ba70b3  paper/er-epr-six-protocols-2026-v2.pdf  (v2)
sha256: e83f259468b4e62bb59edcf9d209ace70936ecea800cb4ed632c0a32ff91bcdd  er-epr-six-protocols-2026.pdf     (v1, superseded)
```

You can also check the hash in the browser at [qubistry.co/#er-epr](https://www.qubistry.co/#er-epr).

## Cite

Use the **"Cite this repository"** button (from `CITATION.cff`) or the Zenodo DOI.

---

**En español:** seis experimentos en ibm_marrakesh sobre las firmas de frontera de la conjetura ER=EPR. Cada resultado trae su Job ID de IBM para que cualquiera pueda bajar el dato crudo. Lo medido está en la tabla; la lectura gravitacional es interpretación. La versión 2 corrige el Experimento 6.
