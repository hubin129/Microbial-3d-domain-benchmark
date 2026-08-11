[THIRD_PARTY_SOURCES.md](https://github.com/user-attachments/files/30919388/THIRD_PARTY_SOURCES.md)
# Third-Party Software Sources

This file maps the third-party software archives supplied with the protocol to their original projects. The links are provided for provenance, installation updates, license review, issue reporting, and citation. The archived copies remain governed by their upstream licenses.

## Chromosomal-Domain Callers

| Method | Archive in `tools/13-methods.zip` | Archived version | Upstream source | Reported license | Original publication |
|---|---|---|---|---|---|
| Armatus | `Armatus.zip` | v1.0, commit `ea54a41` | https://github.com/kingsfordgroup/armatus | BSD-3-Clause | Filippova et al., *Algorithms for Molecular Biology* (2014) |
| Arrowhead | `Arrowhead.zip` | Juicer Tools v2.09.00 | https://github.com/aidenlab/juicer | MIT | Rao et al., *Cell* (2014) |
| HiTAD | `HiTAD.zip` | TADLib v0.5.0 | https://github.com/XiaotaoWang/TADLib | MIT | Wang et al., *Nucleic Acids Research* (2017) |
| Matryoshka | `matryoshka.zip` | v0.1.0 | https://github.com/COMBINE-lab/matryoshka | BSD-3-Clause | Malik and Patro, *IEEE/ACM Transactions on Computational Biology and Bioinformatics* (2019) |
| OnTAD | `OnTAD.zip` | v1.0 | https://github.com/anlin00007/OnTAD | GPL-3.0 | An et al., *Genome Biology* (2019) |
| TADpole | `TADpole.zip` | v1.0 | https://github.com/3DGenomes/TADpole | GPL-3.0 | Soler-Vila et al., *Nucleic Acids Research* (2020) |
| SpectralTAD | `SpectralTAD.zip` | Bioconductor v1.2.0 | https://bioconductor.org/packages/SpectralTAD | GPL-3.0 | Cresswell and Dozmorov, *BMC Bioinformatics* (2020) |
| deDoc | `deDoc.zip` | v1.0 | https://github.com/yinxc/structural-information-minimisation | MIT | Li et al., *Nature Communications* (2018) |
| SuperTAD-fast | `SuperTAD.zip` | v1.0 | https://github.com/deepomicslab/SuperTAD | MIT | Zhang et al., *Journal of Computational Biology* (2024) |
| TADtree | `TADtree.zip` | v1.0 | https://compbio.cs.brown.edu/projects/tadtree/ | GPL-3.0 | Weinreb and Raphael, *Bioinformatics* (2016) |
| rGMAP | `GMAP.zip` | v1.4 | https://github.com/wbaopaul/rGMAP | GPL-2.0 | Yu et al., *Nature Communications* (2017) |
| HiCKey | `HiCKey.zip` | v1.0 | https://github.com/YingruWuGit/HiCKey | MIT | Xing et al., *BMC Bioinformatics* (2021) |
| GRiNCH | `GRiNCH.zip` | v1.0 | https://github.com/Roy-lab/grinch | MIT | Lekschas et al., *Genome Biology* (2021) |

## Additional Third-Party Software

| Software | Archive or environment entry | Upstream source | Reported license | Primary reference |
|---|---|---|---|---|
| EVRC | `tools/EVRC-main.zip` | https://github.com/mbglab/EVRC | GPL-3.0 | Wang et al., *Bioinformatics* (2023), https://doi.org/10.1093/bioinformatics/btad638 |
| coolpuppy / coolpup.py | `coolpuppy==1.1.0` in `environment/requirements.txt` | https://github.com/open2c/coolpuppy | MIT | Flyamer et al., *Bioinformatics* (2020), https://doi.org/10.1093/bioinformatics/btz540 |

## Redistribution Notes

- The caller and EVRC archives are included as separate packages and are not incorporated into the benchmark analysis code.
- Upstream licenses apply to the corresponding third-party files. The license label in this table is a provenance summary and does not replace the full upstream license text.
- Users should review the current upstream repository before redistribution because licensing, dependencies, and installation instructions may change after the archived version.
- Publications should cite the original paper for every third-party program actually used.

