# Supplementary Protocol: Caller Parameters and Environment

## 1. Execution Environment

All callers were run on an Ubuntu 20.04.2 LTS workstation with an Intel Xeon W-2175 2.50 GHz CPU and 200 GB RAM. Runtime and peak memory were recorded by the Python monitor. The monitor launched method-level *E. coli* wrappers with `subprocess`, measured wall-clock time with `time.time`, and sampled combined parent-plus-descendant RSS every 0.5 s. A wrapper can process multiple resolutions sequentially, so the recorded runtime is the complete wrapper runtime rather than a standardized per-condition value.

Python scripts used Python 3.8-3.10, R scripts used R 4.0-4.2, Java methods used OpenJDK 11, and C++ methods were compiled with GCC 9-11. Method-specific dependencies are listed by the upstream projects in `THIRD_PARTY_SOURCES.md`.

## 2. Caller Parameters

Unless stated otherwise, parameters were identical across species and resolutions. `Default` means the original software default was used without modification.

### Armatus

```text
armatus -S -i <matrix> -N -g 0.1 -m -r <res> -c <chr> -n 1 -o <output> -s 0.05
```

`-S` selects sparse symmetric input, `-N` preserves input normalization, `-g 0.1` sets maximum gamma, `-m` requests multiscale output, `-r` supplies resolution, `-c` supplies chromosome, `-n 1` selects one-copy mode and `-s 0.05` sets the gamma step. Whole-genome mode omits `-c`.

### Arrowhead

```text
java -jar juicer_tools_2.09.00.jar arrowhead -c <chr> -r <res> -k NONE <input.hic> <output>
```

`-k NONE` prevents a second normalization because the input `.hic` files already contain ICE-balanced values. Other options use Arrowhead defaults.

### HiTAD

```text
hitad -d <config> -O <output> --exclude chrY --minimum-chrom-size 1 --maxsize 2000000 -W RAW -p 18
```

The maximum domain size is 2 Mb, the minimum chromosome size is 1 bp, `-W RAW` uses matrix values without cool-file weights, and `-p 18` uses 18 threads. For *E. coli* Micro-C at 200 bp, `-p 1` was used.

### Matryoshka

```text
matryoshka -R -i <matrix> -g 0.5 -m -r <res> -c <chr> -n 100 -o <output> -s 0.05
```

`-R` selects Rao sparse input, `-g 0.5` sets maximum gamma, `-m` requests multiscale output, `-n 100` sets the minimum sample count and `-s 0.05` sets the gamma step.

### OnTAD

```text
OnTAD <matrix> -penalty 0.1 -maxsz <M> -minsz <m> -o <output> -bedout <id> <max_pos> <res>
```

The physical size bounds are 30 kb and 2 Mb and are converted to bins at each resolution. The resulting pairs `(maxsz, minsz)` are `(10000,150)` at 200 bp, `(4000,60)` at 500 bp, `(2000,30)` at 1,000 bp, `(1000,15)` at 2,000 bp, `(400,6)` at 5,000 bp and `(200,3)` at 10,000 bp. `penalty 0.1` is the default.

### TADpole

```text
TADpole(input_data, chr=<chr>, start=0, end=<N*res>, resol=<res>)
```

Only chromosome, start, end and resolution are supplied; all other parameters retain defaults. All yeast nuclear chromosomes are analyzed independently. Under the benchmark settings, TADpole produced domains in 118 of 119 chromosome tasks.

### SpectralTAD

```text
SpectralTAD(x, chr=<chr>, levels=<L>, resolution=<res>, qual_filter=FALSE)
```

The maximum hierarchy is selected from matrix size: 1-10 levels for at least 4,000 rows, 1-8 for at least 2,000, 1-6 for at least 1,000, 1-4 for at least 400 and 1-2 otherwise. Quality filtering is disabled. Yeast chromosomes shorter than 2 Mb are excluded by the method's internal filter; *E. coli* uses 10 levels.

### deDoc

```text
java -jar deDoc.jar <input_file>
```

deDoc accepts no command-line parameters and uses its default automatic detection behavior. Input coordinates are one-based sparse-matrix coordinates.

### SuperTAD-fast

```text
SuperTAD multi <matrix> --fast -r <res> --chrom1 <chr> --window <W> --step <S> -w <output>
```

The fast mode is used. For Hi-C, `window=5` and `step=200` or the matrix row count when smaller. For Micro-C, `window=20` and `step=10` or the matrix row count when smaller.

### TADtree

The contact threshold is `S = 100/(res/1000)`: 200 at 500 bp, 100 at 1,000 bp, 50 at 2,000 bp, 20 at 5,000 bp and 10 at 10,000 bp. Other settings are `M=10`, `p=3`, `q=12`, `gamma=100` and `N=50`. The original default `N=100` was reduced to control runtime. Timeout and zero-output states are retained.

### rGMAP (GMAP in the manuscript)

```text
rGMAP(get_data, resl=<res>, max_d=20, min_d=5, dom_order=2)
```

All parameters follow the package example defaults. Yeast analysis includes chr1-chr16 and excludes the mitochondrial chromosome.

### HiCKey

```text
hickey <config_file>
```

The configuration contains the one-based sparse-matrix path, the precomputed Brownian background model, resolution, chromosome count (1 for each independent run), `p=0.05` and boundary `FDR=0.00005`.

### GRiNCH

GRiNCH is run three times to obtain the TAD, subTAD and metaTAD levels:

```text
grinch <matrix> <bed> -e 20000 -o <output>_TAD
grinch <matrix> <bed> -e 10000 -o <output>_subTAD
grinch <matrix> <bed> -e 40000 -o <output>_metaTAD
```

The three fixed `-e` values follow the example configuration.

## 3. Matrix Preprocessing

Matrices are binned at the target resolution and converted to dense, three-column sparse, Rao, deDoc, `.hic` or `.cool` formats as required by each caller. Conversion changes file organization but not genomic coordinates or target bin size. All matrices are ICE-balanced. Dense, `.hic` and `.cool` files derive from the corresponding ICE-balanced matrix. Downstream Fold-change reads balanced values from canonical `.cool` files; EVRC uses the corresponding balanced dense matrix.

## 4. Execution States

The recorded states are valid output, completed with zero calls, OOM, Timeout, unsupported input and missing. Timeout is defined as more than 168 h. All states remain in the main figure and supplementary tables. Key states include no usable TADtree output, OOM for SuperTAD-fast on *E. coli*, internal 2 Mb filtering of all yeast chromosomes by SpectralTAD and five Armatus calls across four conditions.

