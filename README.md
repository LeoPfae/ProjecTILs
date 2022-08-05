# Interpretation of T cell states using reference single-cell atlases

<p align="center">
  <img height="80" src="docs/RSticker_ProjecTILs.png">
</p>

`ProjecTILs` is a computational method to project scRNA-seq data into reference single-cell atlases, enabling their direct comparison in a stable, annotated system of coordinates.

In contrast to other methods, ProjecTILs allows not only accurately embedding new scRNA-seq data into a reference without altering its structure, but also characterizing previously unknown cell states that “deviate” from the reference. ProjecTILs accurately predicts the effects of cell perturbations and identifies gene programs that are altered in different conditions and tissues.

![ProjecTILs_pipeline](https://github.com/carmonalab/ProjecTILs/blob/dev/docs/Pipeline_projecTILs.png?raw=true)

`ProjecTILs` comes with ready-to-use [reference T cell atlases](#reference-atlases) for cancer and viral infection, and can be also used with custom, user-generated references (see [Building a custom reference atlas for ProjecTILs](https://carmonalab.github.io/ProjecTILs.demo/build_ref_atlas.html))

For real-life applications, check out our list of [ProjecTILs Case Studies](https://carmonalab.github.io/ProjecTILs_CaseStudies/)

Find the installation instructions for the package below, and a vignette detailing its functions at [Tutorial (html)](https://carmonalab.github.io/ProjecTILs.demo/tutorial.html) and [Tutorial (repository)](https://github.com/carmonalab/ProjecTILs.demo)

If you prefer to avoid installing R packages, you can run `ProjecTILs` in Docker. A ready-to-use Docker image with usage instructions is available on [DockerHub](https://hub.docker.com/repository/docker/mandrea1/projectils_demo) (might not include the latest version)

### Package Installation

To install `ProjecTILs` directly from its Git repository, run the following code from within R or RStudio:
```
install.packages("remotes")
library(remotes)

remotes::install_github("carmonalab/scGate")
remotes::install_github("carmonalab/ProjecTILs")
```

### Test the package

Load sample data and test your installation:
```
library(ProjecTILs)
data(query_example_seurat)

make.projection(query_example_seurat)
```

On your first run, the `make.projection` call will download the reference TIL atlas used as default map. This may take some time depending on your connection, but it is only necessary on the first run.


### Data projection TUTORIAL

Find a step-by-step tutorial for `ProjecTILs` at: [ProjecTILs tutorial](https://carmonalab.github.io/ProjecTILs.demo/tutorial.html)

To run the code of the tutorial on your machine, download the demo repository: [ProjecTILs tutorial repo](https://github.com/carmonalab/ProjecTILs.demo) or obtain a [Docker image](https://hub.docker.com/repository/docker/mandrea1/projectils_demo) with all dependencies pre-installed.

For real-life applications, check out our list of [ProjecTILs Case Studies](https://carmonalab.github.io/ProjecTILs_CaseStudies/)

### Documentation

See a description of the functions implemented in ProjecTILs at: [ProjecTILs functions](docs/functions.md)

### Reference Atlases

Reference atlases are generated by comprehensive scRNA-seq multi-study integration and curation, and describe reference cell subtypes in a specific biological context.

Currently available atlases:


* **tumor-infiltrating T lymphocytes (TIL) atlas**: consists of 16,803 high-quality single-cell transcriptomes from 25 samples (B16 melanoma and MC38 colon adenocarcinoma tumors) from six different studies. Available at: [https://doi.org/10.6084/m9.figshare.12478571](https://doi.org/10.6084/m9.figshare.12478571) and interactively at [https://spica.unil.ch/refs/TIL](https://spica.unil.ch/refs/TIL)

* **acute and chronic viral infection CD8 T cell atlas**: consists of 7,000 virus-specific CD8 T cells from 12 samples (spleen) from different timepoints (day 4.5, day 7/8 and day 30) from mice infected with lymphocytic choriomeningitis virus (LCMV) Arm (acute infection) or cl13 (chronic infection) strains. Available at: [https://doi.org/10.6084/m9.figshare.12489518](https://doi.org/10.6084/m9.figshare.12489518) and interactively at [https://spica.unil.ch/refs/viral-CD8-T](https://spica.unil.ch/refs/viral-CD8-T)

* **acute and chronic viral infection CD4 T cell atlas**: consists of over 35,000 high-quality virus-specific (GP66:I-Ab+) CD4 T cells from 11 samples (spleen) from different timepoints following LCMV Armstrong or Clone 13 viral infection (7 or 21 days after Clone 13 infection, and 7, 21 and >60 days after LCMV Armstrong infection). Available at: [https://doi.org/10.6084/m9.figshare.16592693](https://doi.org/10.6084/m9.figshare.16592693) and interactively at [https://spica.unil.ch/refs/viral-CD4-T](https://spica.unil.ch/refs/viral-CD4-T)

If you wish to use your own **custom reference atlas**, follow this vignette to prepare it in a format that can be understood by ProjecTILs: [Building a custom reference atlas for ProjecTILs](https://carmonalab.github.io/ProjecTILs.demo/build_ref_atlas.html)

### SPICA online portal

You can now explore our atlases interactively and project your data through the [SPICA web portal](https://spica.unil.ch/). Find some tutorials for interacting with SPICA at [https://spica.unil.ch/tutorials](https://spica.unil.ch/tutorials)

### Troubleshooting 

* If *load.reference.map()* fails with error "Reference object X is invalid" the first time you run it; it is likely that reference atlas download has failed due to Timeout. Try setting ```options(timeout = max(300, getOption("timeout")))``` to increase download Timeout.

* If a warning message prevented *remotes* from installing the package, try:
```Sys.setenv(R_REMOTES_NO_ERRORS_FROM_WARNINGS="true")```

* For analyzing datasets composed of multiple batches (e.g. different subjects, technologies), we recommend projecting each batch separately, by providing ProjecTILs a list of Seurat objects as input, e.g.:
```
data.seurat.list <- SplitObject(data.seurat, split.by = "batch")
query.projected.list <- make.projection(data.seurat.list)
```




### Citation

**Interpretation of T cell states from single-cell transcriptomics data using reference atlases** Massimo Andreatta, Jesus Corria-Osorio, Soren Muller, Rafael Cubas, George Coukos,  Santiago J Carmona. *Nature Communications* **12** Article number: 2965 (2021) - https://www.nature.com/articles/s41467-021-23324-4

<p align="center">
  <img height="80" src="docs/RSticker_ProjecTILs.png">
</p>
