# SSRF vs. Developers: A Study of SSRF-Defenses in PHP Applications

This organization contains the toolchain used for our paper.
On a high-level it is made out of two layers:
1. Bytecode PHP code property graph (CPG) generation
2. `SURFER`: A tool to find SSRF candidates in these CPGs.

Cite us via: 
```
@inproceedings{USENIX:Wessels:2024,
 author = {Wessels, Malte and Koch, Simon and Pellegrino, Giancarlo and Johns, Martin},
 booktitle = {33rd USENIX Security Symposium (USENIX Security 2024)},
 organization = {Usenix},
 title = {SSRF vs. Developers: A Study of SSRF-Defenses in PHP Applications},
 tool = {https://github.com/SSRF-vs-Developers},
 url = {https://www.ias.tu-bs.de/publications/ssrf-usenix-2024.pdf},
 year = {2024}
}

```
## CPG Generation
For recent versions, check out the sister organization: https://www.github.com/PHP-CPG/

The corresponding author for the CPG generator is Simon Koch. 

To use our specific versions, e.g., for the academic artifact evaluation, use the Dockerfiles provided in https://github.com/SSRF-vs-Developers/CpgGeneration.
They use pinned versions.

## `SURFER`
https://github.com/SSRF-vs-Developers/surfer

## Build Instructions
Preamble: These instructions pull the latest versions of our toolchain as dependencies.
To use the fixed versions, replace steps 1) - 2) with cloning `git clone git@github.com:SSRF-vs-Developers/CpgGeneration.git` instead and calling the `.create.sh` scripts in the same order as below. (PHP, CPG, experiment runner/scala-master).


0. Setup
    - Use a linux-based system
    - Install docker, git

1. PHP-CPG
    - Clone it:`git clone git@github.com:PHP-CPG/CPG.git`
    - Build docker for our patched PHP
        - `cd resources/docker/PHP-StringPatched`
        - `./create.sh`
        - This step build PHP twice. This may take a while depending on your system.
    - Build docker for the CPG creation
        - `cd ../multilayer-php-cpg`
        - `./create.sh`
        - This builds and tests our bytecode CPG generator
        - Optional: Use it.
            - `docker run --rm -it multilayer-cpg-php`
            - `./php2cpg <path-to-php-file-or-project> bytecode 8`
2. Experiment Runner Setup
    - `cd ..`
    - `git clone git@github.com:PHP-CPG/scala-master.git`
    - `cd resources/docker/template`
    - `./create.sh`
    - This creates and tests our instrumentation for creating CPGs and running CPG consumers on them.

3. Clone Surfer
    - Clone it: `git clone git@github.com:SSRF-vs-Developers/surfer.git`
    - Build docker
        - `cd resources/docker`
        - `./create.sh`
    - Run the pipeline:
        - Go to the root level of this repo.
        - `./surfer_docker_run.sh <absolute-path-to-folder-of-projects> <folder-for-cpgs> <folder-for-output>
        - the output folder now contains JSON files containing SSRF candidate flows
        - the input folder must be a folder of folders
            - e.g.:
```
subjects:
    - project_a
        - file.php
        - src/
    - project_b
        -file.php
```

      
