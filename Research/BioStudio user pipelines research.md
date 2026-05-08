# BioStudio user pipelines research

This document maps specific biological scientist user types in BioStudio to the pipelines they are most likely to use.

## User to pipeline mapping

| Users | Pipeline |
| --- | --- |
| Single-cell analysis scientist | Ask BioStudio to run or guide single-cell analysis on a study<br>↓<br>LLM parses assay type, analysis stage, and expected output<br>↓<br>BioFlex calls project, data access, notebook/app, and visualization functions<br>↓<br>Single-cell results, plots, and saved study artifacts |
| Spatial omics analyst | Ask to process or explore spatial transcriptomics/proteomics data<br>↓<br>LLM parses spatial workflow intent and required input assets<br>↓<br>BioFlex calls file retrieval, environment, notebook/app, and result rendering functions<br>↓<br>Spatial maps, annotations, and stored outputs |
| Single-cell immunology scientist | Ask BioStudio to analyze immune cell populations from single-cell data<br>↓<br>LLM parses immune profiling intent, cohort context, and output need<br>↓<br>BioFlex calls data access, notebook/app, clustering, annotation, and visualization functions<br>↓<br>Immune cell composition, marker signatures, and saved study outputs |
| Cancer genomics scientist | Ask to explore tumor datasets, variants, or molecular subtypes<br>↓<br>LLM parses cancer study intent and requested analysis layer<br>↓<br>BioFlex calls project retrieval, sequencing analysis, notebook/app, and plotting functions<br>↓<br>Tumor-focused findings, subtype views, and stored results |
| Translational biomarker scientist | Request biomarker discovery or cohort comparison analysis<br>↓<br>LLM parses biomarker goal, sample groups, and evidence criteria<br>↓<br>BioFlex calls catalog search, cohort filtering, notebook analysis, and result summarization functions<br>↓<br>Candidate biomarkers and comparison outputs |
| Spatial biology scientist | Ask to inspect cell neighborhoods, tissue regions, or spatial expression patterns<br>↓<br>LLM parses tissue context and spatial analysis objective<br>↓<br>BioFlex calls spatial data retrieval, notebook/app workflow, and visualization functions<br>↓<br>Spatial maps, region annotations, and interpretable tissue insights |
| Cell therapy scientist | Ask to evaluate engineered cell product quality or functional signatures<br>↓<br>LLM parses cell therapy study intent and relevant QC/phenotype needs<br>↓<br>BioFlex calls project data access, analysis notebook/app, and result visualization functions<br>↓<br>Cell product characterization outputs and tracked artifacts |
| CRISPR screening scientist | Ask to analyze perturbation screening results and hit candidates<br>↓<br>LLM parses screen type, perturbation context, and ranking objective<br>↓<br>BioFlex calls screening data retrieval, notebook/app execution, and hit summarization functions<br>↓<br>Ranked hits, effect summaries, and saved analysis outputs |
| Proteomics scientist | Ask to process protein abundance data or compare protein signatures across samples<br>↓<br>LLM parses proteomics workflow intent and comparison target<br>↓<br>BioFlex calls file retrieval, environment, notebook/app, and plotting functions<br>↓<br>Differential protein results and reusable visual outputs |
| Multi-omics integration scientist | Ask to integrate transcriptomics, proteomics, or epigenomics from the same study<br>↓<br>LLM parses cross-modality integration goal and expected output<br>↓<br>BioFlex calls multi-dataset retrieval, notebook execution, and integration workflow functions<br>↓<br>Integrated multi-omics views and study-level findings |
| Disease area scientist | Ask BioStudio to compare disease vs control biology in a target indication<br>↓<br>LLM parses disease context, cohort definition, and biological question<br>↓<br>BioFlex calls catalog search, project data access, notebook analysis, and result visualization functions<br>↓<br>Disease-relevant patterns and comparison outputs |
| Biomarker validation scientist | Ask to verify whether a known marker or signature is reproducible in a new cohort<br>↓<br>LLM parses validation intent, target signature, and acceptance criteria<br>↓<br>BioFlex calls cohort retrieval, notebook/app validation workflow, and summary functions<br>↓<br>Validation evidence and reproducibility results |
| Mechanism-of-action scientist | Ask to characterize pathway or target-level effects after treatment or perturbation<br>↓<br>LLM parses treatment context, target hypothesis, and mechanism question<br>↓<br>BioFlex calls project data retrieval, notebook analysis, pathway interpretation, and visualization functions<br>↓<br>Mechanistic insights and supporting analysis outputs |
| Preclinical research scientist | Ask to analyze experimental study data from model systems or preclinical cohorts<br>↓<br>LLM parses experiment design, model context, and analysis objective<br>↓<br>BioFlex calls study data retrieval, notebook/app workflow, and reporting functions<br>↓<br>Preclinical study results and reusable outputs |
| Clinical translational scientist | Ask to review patient-linked molecular data for translational interpretation<br>↓<br>LLM parses patient cohort context and translational analysis goal<br>↓<br>BioFlex calls permission-aware data access, notebook analysis, and result summarization functions<br>↓<br>Clinically relevant molecular insights within governed access |
| Wet-lab biology scientist | Ask to open a prepared study, inspect results, or run a guided analysis without heavy coding<br>↓<br>LLM parses guided-use intent and available study context<br>↓<br>BioFlex calls launcher, project, result-view, and prepared notebook/app functions<br>↓<br>Accessible biological outputs without deep technical setup |

## Notes

- A single person can belong to more than one user type depending on disease area, assay type, and study context.
- In BioStudio, actual behavior is shaped by workspace context, granted permissions, project scope, data availability, and environment support.
- Catalogs, Projects, File Browser, Environment, Debugger, Members, and Requests are the main modules that define these pipelines.

#bioturing #biostudio #research #user-behavior #pipeline #persona
