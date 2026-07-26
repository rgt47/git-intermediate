# Intermediate Git for Biostatistics: A Three-Day Bridge
*2026-07-25 17:56 PDT*

A short second course in version control for graduate
biostatistics students, situated between the Git boot camp
and the Biostatistics Practicum. Three days, one chapter
each. Prerequisite: *Git and GitHub for Biostatistics: A
One-Week Boot Camp*.

## Structure

- **Day 1** Selective Staging and Work in Progress
- **Day 2** Rewriting History
- **Day 3** Recovery and Forensics

Each day is approximately 1 hour of lecture content + 2
hours of homework with worked solutions. No examinations.

## Build

```bash
quarto render
```

The cover is generated procedurally:

```bash
Rscript images/build-cover.R
```

## Position in the series

This bridge is a preparatory companion, alongside the two
boot camps, to the graduate biostatistics sequence:

- *Git and GitHub for Biostatistics* — the prerequisite
  boot camp
- *R for Biostatistics* — the parallel R boot camp
- *Biostatistics Practicum* — workflow infrastructure, which
  this bridge feeds

## License

Prose: CC BY-NC-ND 4.0. Code: CC0 1.0.
