# SSRF vs. Developers: A Study of SSRF-Defenses in PHP Applications

This organization contains the toolchain used for our paper.
On a high-level it is made out of two layers:
1. Bytecode PHP code property graph (CPG) generation
2. `SURFER`: A tool to find SSRF candidates in these CPGs.

Cite us via: 
```
@inproceedings{USENIX:Wessels:2024,
  title={SSRF vs. Developers: A Study of SSRF-Defenses in PHP Applications}
  authors={Wessels, Malte and Koch, Simon and Pellegrino, Giancarlo and Johns, Martin},
  venue={USENIX Security},
  year={2024}
}
```
## CPG Generation
For recent versions, check out the sister organization: https://www.github.com/PHP-CPG/

To use our specific versions, e.g., for the academic artifact evaluation, use the Dockerfiles provided in https://github.com/SSRF-vs-Developers/CpgGeneration.
They use pinned versions.

## `SURFER`
https://github.com/SSRF-vs-Developers/surfer

## Build Instructions
todo

