# platforms for reproducibility 

overview of available options

---

### what tools are available 

- for ad hoc workflows and tools: docker and singularity
- for lightweight application: jupyter notebooks
- for pipelines: shell scripts in github   
- for software tools: bioconda/biocontainer  

---
### devops 

- software development + software operations
- automate and monitor

---

![Devops Explained](https://hostadvice.com/wp-content/uploads/2018/03/devopsext.jpg)

---

![Containers VMs](https://zdnet2.cbsistatic.com/hub/i/r/2017/05/08/af178c5a-64dd-4900-8447-3abd739757e3/resize/770xauto/78abd09a8d41c182a28118ac0465c914/docker-vm-container.png)
https://www.zdnet.com/article/what-is-docker-and-why-is-it-so-darn-popular/

---

### virtualisation
pros and cons

- ++ very similar to a full OS
- ++ high OS diversity
- -- need of more space and resources
- -- slower than containers
- -- not as good automation

---

### containers
pros and cons

- ++ faster
- ++ no need for full OS
- ++ easy solutions for distribution of recipes. high portability
- ++ easy to automate
- -- still OS dependant solutions
- -- not real OS in some cases

---

### Docker

![Docker](https://msdnshared.blob.core.windows.net/media/2017/10/docker.png)

---

### Docker

- platform for developing, shipping, and running applications
- infrastructure as application/code
- Open Container Initiative
- Docker community edition

---

![Docker components](https://docs.docker.com/engine/images/architecture.svg)

---

### Docker image

- read-only templates
- containers are run from them
- images are not run
- images have several layers

---

### Docker image - building

- can be built from existing images
  - ubuntu, alpine
- any modification from base image is a new layer ( tip: use && )
- base images can be created with tools such as Debootstrap
- images have several layers
---

### Docker image - instructions

- Recipe: Dockerfile
- Instructions
- FROM
- ADD, COPY
- RUN
- ENV PATH, ARG
- USER, WORKDIR, LABEL
- VOLUME, EXPOSE
- CMD, (ENTRYPOINT)

[Reference](https://docs.docker.com/engine/reference/builder/)

---

### ** One tool, one container **

- start from packages e.g. pip/PyPI, CPAN, or CRAN
- use versions for tools and containers
- use ENV PATH instead of ENTRYPOINT
- reduce size as much as possible
- keep data outside the container
- check the license
- make your container discoverable e.g. biocontainers, quay.io, docker hub

---

### Example

```bash
FROM biocontainers/biocontainers:v1.0.0_cv4

LABEL base_image=“biocontainers:v1.0.0_cv4”

LABEL version=“3”

LABEL software=“Comet”

LABEL software.version=“2016012”

LABEL about.summary=“an open source tandem mass spectrometry sequence database search tool”

LABEL about.home=http://comet-ms.sourceforge.net

LABEL about.documentation=http://comet-ms.sourceforge.net/parameters/parameters_2016010

LABEL about.license_file=http://comet-ms.sourceforge.net

LABEL about.license=“SPDX:Apache-2.0”

LABEL extra.identifiers.biotools=“comet”

LABEL about.tags=“Proteomics”

LABEL maintainer=“Felipe da Veiga Leprevost <felipe@leprevost.com.br>”

USER biodocker

RUN ZIP=comet_binaries_2016012.zip && wget https://github.com/BioDocker/software-archive/releases/download/Comet/$ZIP-O/tmp/$ZIP&&unzip/tmp/$ZIP-d/home/biodocker/bin/Comet/&&chmod-R 755/home/biodocker/bin/Comet/*&&rm/tmp/$ZIP

RUN mv/home/biodocker/bin/Comet/comet_binaries_2016012/comet.2016012.linux.exe/home/biodocker/bin/Comet/comet

ENV PATH /home/biodocker/bin/Comet:$PATH

WORKDIR /data/
```
---
### recommendations ###

- Carefully define a set of tools for a given analysis
- Use tools from the Bioconda registry
- Adopt containers to guarantee consistency of results
- Use virtualization to make analyses “resistant to time”.

---

![reproducibility stack](http://data.bits.vib.be/pub/trainingen/CommunityMeeting/20180627-reproducibility-stack.png)

---

### Further reading ###

- [impact of docker containers on performance](https://peerj.com/articles/1273/)
- [container-based virtualization for HPC environments](https://arxiv.org/abs/1709.10140)
- recommendations on [containers](https://f1000research.com/articles/7-742/v1)
- [practical computational reproducibility in life sciences](https://www.biorxiv.org/content/early/2017/10/11/200683)

---

# Thanks

- Bioinfo Core at CRG  [slides](https://github.com/biocorecrg/C4LWG-2018/tree/master/slides)
- based on recommendation from [F1000](https://f1000research.com/articles/7-742/v1)
