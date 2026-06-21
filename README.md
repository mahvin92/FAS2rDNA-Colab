> **Announcement:** Starting 2026 June 15, support ofr FAS2rDNA-Colab is now moved to FAS2rDNA Web, our most capable cloud-implementation yet without the need to install or setup a jupyter notebook. FAS2rDNA Web is accessible [through our website](https://fas2rdna.chordexbio.com/)

# FAS2rDNA-Colab
Colab-friendly implementation of [FAS2rDNA](https://github.com/mahvin92/FAS2rDNA).

<img width="100" height="100" alt="FAS2rDNA logo" src="https://github.com/mahvin92/FAS2rDNA-Colab/blob/main/asset/FAS2rDNA%20logo/1.png" />
FAS2rDNA is a lightweight, assembly‑aware reconstruction engine that converts genomic coordinates and annotations into multi-FASTA sequences. It supports short fragments to large regions (genes, isoforms, loci) across multiple species and assemblies, using a simple tabular input format that is optimized for downstream analytics and machine learning workflows.


#### Links:

Launch [FAS2rDNA-Colab on Google Colaboratory](https://fas2rdna.chordexbio.com/colab-access)

Read the protocol here: [Protocols.io](https://dx.doi.org/10.17504/protocols.io.14egn1xr6v5d/v1)

Visit the official wesite here: [FAS2rDNA by ChordexBio](https://fas2rdna.chordexbio.com/)

## FAS2rDNA-Colab Usage
### 1. Preparing your data
#### a. Data format:
i) Obtain and compile your genomic annotations and coordinates in a table and format your columns to contain the following column headers:
- sample_id: the identifier of your sample (e.g., sample source)
- seq_loc: the genomic coordinate of your sequence (see below for standards)
- seq_id: the identifier of the sequence (e.g., gene name)
- description: any information about the sequence entry

Table 1. Sample data format.
| sample_id | seq_loc | seq_id | description |
| :--- | :--- | :--- | :--- |
| BLOOD_001 | hg19:9:106938220-106938244:+ | TP53 | Tumor protein p53; genomic locus on chromosome 17. |
| LIVER_A2 | hg38:11:86938550-86938664:- | BRCA2 | DNA repair protein; captured via targeted enrichment. |
| SKIN_NS | hg18:7:96998253-97038145:+ | BRAF | Proto-oncogene; wild-type sequence from control group. |
| BONE_M | hg19:1:76938211-76949381:- | NRAS | Neuroblastoma RAS viral oncogene homolog. |

*- Note that you can have additional headers as long as you have all the required column headers, listed above.*

ii) Save your file in a tab-delimited text file (.txt or .tsv). ```File --> Save As ---> TXT or TSV --> Save```

#### b. Standard genomic coordinate:
The seq_loc field MUST assume ONLY the following format: ```genome_assembly:chromosome_number:DNA_location:strand_location```, as shown in the Figure 1 below:. For example, the coordinate 'hg19:9:106938220-106938244:+' (as exemplified in Table 1) is to be reconstructed using the hg19 genome assembly, chromosome 9, DNA locations 106938220-106938244 nt, in the positive sense strand.

<img width="500" height="345" alt="FAS2rDNA coordinate" src="https://github.com/user-attachments/assets/bb80b03c-2703-4c8b-a6f0-f6c0a847af47" />

*Figure 1. Standard format for the genomic coordinate in column seq_loc of your data.*


### 2. Performing a multi-FASTA reconstruction
#### a. Launching the software:
The FAS2rDNA-Colab can be opened in several ways:

i) Launch from the shareable link here: [FAS2rDNA-Colab](https://fas2rdna.chordexbio.com/colab-access)

ii) Download the FAS2rDNA-Colab notebook from the ```ipynb``` folder on [GitHub/FAS2rDNA-Colab](https://github.com/mahvin92/FAS2rDNA-Colab/tree/main/ipynb) and manually upload that in your Colab workspace ```File --> Upload Notebook```.

iii) Load FAS2rDNA-Colab directly from an opened Colab notebook by running the code below:
```
from IPython.display import HTML

notebook = "FAS2rDNA-colab_v1_0.ipynb" # -> change the version here
repo = "mahvin92/FAS2rDNA-Colab"
folder = "ipynb"

colab_url = f"https://colab.research.google.com/github/{repo}/blob/main/{folder}/{notebook}"
HTML(f'<a href="{colab_url}" target="_blank">Open {notebook} in Google Colab</a>')

```

#### b. Running FAS2rDNA-Colab
i) Type the name of your experiment in the ```Project_name``` field

ii) Click ```Runtime``` and select ```Run all```

iii) Upload your files by clicking ```Choose Files``` below the cell block in ```Step 1. Upload data```

iv) Wait for the run to complete

v) Results will be automatically downloaded or manually get them from ```/content/fas2rdna/outputs```

#### c. Validating the results
FAS2rDNA-Colab returns two types of data:

i) the individual .fasta file from multiple txt inputs

ii) the combined .fasta file, compiling all multi-FASTA sequences in one file.

Sample result:
```
>BLOOD_001
AAATCGGCGGACTCGGCAC ...
>LIVER_A2
TTTAAACGCCCCCACGCCT ...
>SKIN_NS
GGGCGCGTTACGTGCACGT ...
>BONE_M
TGCATTGACACCACTTCGG ...
```

## Supported Assemblies
The following genome assemblies are currently supported in the v.1.0 of FAS2rDNA-Colab (FAS2rDNA will detect them automatically). For more information, please refer to: [UCSC Genome Browser](https:.genome.ucsc.edu/cgi-bin/hgGateway).

- Human: hg16, hg17, hg18, hg19, hg38, hs1
- Mouse: mm7, mm8, mm9, mm10, mm39
- Rat: rn4, rn5, rn6, rn7
- Zebrafish: danRer7, danRer10, danRer11
- Fruit Fly: dm2, dm3, dm6
- *C. elegans*: ce4, ce6, ce10, ce11
- Yeast (*S. cerevisiae*): sacCer1, sacCer2, sacCer3

## Troubleshooting
##### 1. No FASTA output generated
- Verify that output directories exist, unchanged, and all cells/steps are sequentially executed.
- Confirm that the *seq_loc* column exists in your data and all assemblies referenced in are supported or validated
- Refresh your File browser to force Colab to load your files

##### 2. FAS2rDNA is skipping entries
- Confirm that those entries contain a valid and well-formatted *seq_loc* data

##### 3. Empty or truncated sequences
- Check coordinate validity (start < end, within chromosome bounds)
- Ensure reference FASTA files are complete and indexed

##### 4. Incorrect strand orientation
- Confirm the strand field in *seq_loc* is correctly specified as + or -

##### 5. Performance bottlenecks with large datasets
- Enable chunked writing or parallel execution
- Split input files by chromosome or sample batches

## Reporting
Comments and suggestions to improve FAS2rDNA-Colab are welcome. If you find any bug or problem, please open an [issue](https://github.com/mahvin92/FAS2rDNA-Colab/issues/new).

## Citation
De los Santos, M.I. (2025). FAS2rDNA-Colab: A cloud-based workflow for pan-cancer, isoform-wide miRNome reconstitution across TCGA cohorts. Protocols.io DOI: 10.17504/protocols.io.14egn1xr6v5d/v1

De los Santos, M. (2025). High-throughput isoform-wide miRNome sequence reconstruction in the TCGA-LUAD cohort using FAS2rDNA. Protocols.io. DOI: 10.17504/protocols.io.rm7vzenqxvx1/v1

## Acknowledgement
FAS2rDNA-Colab is powered by [ChordexBio](https://chordexbio.com/), [FAS2rDNA](https://github.com/mahvin92/FAS2rDNA) and [CodeEnigma](https://github.com/KrishnanSG/codeenigma), made with Python, and tested using Google Colab ❤️

