# MPS run files

The linear programme (LP) of each scenario of this model, as the TIMES model
generator builds it, in MPS format. Any LP solver can read these files, with
no GAMS, Veda or TIMES installation.

The files are attached to the release
[`mps-times-v4.9.7`](https://github.com/esma-ie/OTCGEN/releases/tag/mps-times-v4.9.7) rather than kept in git, so that cloning
this repository stays fast. This folder holds only this description.

## Files

| File | What | Size | SHA-256 |
| --- | --- | --- | --- |
| [`OTCGEN+gc_ref+as_run.mps.gz`](https://github.com/esma-ie/OTCGEN/releases/download/mps-times-v4.9.7/OTCGEN%2Bgc_ref%2Bas_run.mps.gz) | the LP, free MPS, gzipped | 27.3 MB | `b7d3d3d7d8e8744d3689b3f7f3cdd11365e5a6eeb65d57720e95a672cafa6238` |
| [`OTCGEN+gc_ref+as_run.dict.txt.gz`](https://github.com/esma-ie/OTCGEN/releases/download/mps-times-v4.9.7/OTCGEN%2Bgc_ref%2Bas_run.dict.txt.gz) | GAMS names of its rows and columns, gzipped | 6.7 MB | `66e8e540eafa8c59e9a84f2985f85b0c953564fdd2fdd2b71a81d0a83ce7fcb3` |

| Scenario | Rows | Columns | Nonzeros | Objective (CPLEX, in GAMS) |
| --- | --- | --- | --- | --- |
| `gc_ref` | 512,182 | 765,953 | 5,622,500 | 756,404,387.82 |

Rows and columns as GAMS counted them; the rows include the objective equation `EQ_OBJ`.


## How they were made

- **Scenario, "as run":** the run file `dd/gc_ref/gc_ref.run` of this repository, unchanged:
  every option, REDUCE included, as the model sets it.
- **TIMES:** v4.9.7, [etsap-TIMES/TIMES_model](https://github.com/etsap-TIMES/TIMES_model) @ `d9a6a25`.
- **GAMS:** GAMS 54.6.1, the `CONVERT` tool, which writes the model GAMS generated
  for the SOLVE statement: same rows, columns, coefficients, right-hand sides
  and bounds.
- **By:** the reference harness of [TIMES.jl](https://github.com/esma-ie/TIMESjl)
  (`reference/README.md`), the open Julia/JuMP translation of TIMES by ESMA.
  TIMES.jl's checks compare its own LP of each scenario with GAMS's
  `CONVERT` output of these same runs, entry by entry, at 1e-9.

## Reading them

- The objective is a minimisation (`OBJSENSE MIN`) of the single column
  `OBJz`, so its optimal value is the TIMES objective, in the model's
  currency unit.
- GAMS `CONVERT` gives rows and columns generic names: `e1`, `e2`, ... and
  `x1`, `x2`, ... The `.dict.txt.gz` file beside each LP maps them to the TIMES
  names, for example `e1  EQ_OBJ` or `x1  VAR_ACT(REG1,2005,2005,AOTETOT,ANNUAL)`
  (demo12).
- When TIMES moves to a new version, the files are made again and attached to
  a new release (for example `mps-times-v4.9.8`); earlier releases stay.

## Licence

These files are derived from this model and carry its licence,
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). When you use them:

- credit "OTCGEN, Energy Systems Modelling Analytics Ltd (ESMA)" and the original Generative COMET model by the US EPA Office of Research and Development;
- link to the licence and say whether you made changes;
- share your adaptations under the same licence (ShareAlike).
