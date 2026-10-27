# Cowpea trials in North and Northeast Brazil

Versão em português: [README.pt-BR.md](README.pt-BR.md)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23694268.svg)](https://doi.org/10.5281/zenodo.23694268)

2,541 trial results from 61 trials on cowpea (*Vigna unguiculata*, feijão-caupi) in the North and Northeast of Brazil, taken from the tables of 20 open-access Embrapa publications: pests (the leafhopper *Empoasca kraemeri*, *Cerotoma* leaf beetles, the black aphid *Aphis craccivora*, whitefly, the cowpea weevil *Callosobruchus maculatus* in storage and the green stink bug *Nezara viridula*), viruses (cowpea severe mosaic virus, CPSMV; cowpea aphid-borne mosaic virus, CABMV; cucumber mosaic virus, CMV), web blight, *Macrophomina phaseolina* and root-knot nematode, rhizobium inoculation and fertilization, intercropping with maize, irrigation levels, plant density, cultivar and VCU (value for cultivation and use) trials, and the quality of stored grain. Each row is one number exactly as printed, with the page and table it came from, and points to the trial it belongs to.

Cowpea is one of the main foods in the North and Northeast of Brazil, as the introduction of gualter2008 notes. Much of the trial evidence on its pests, diseases and management sits in Embrapa bulletins and journal articles, the oldest from 1978 and five of them scans with a noisy text layer. This dataset makes 20 of them searchable and comparable, from Acre, Roraima and Pará to Maranhão, Piauí, Ceará, Pernambuco, Bahia, Sergipe and Alagoas.

Part of [Paper Rerun](https://paper-rerun.github.io), in its Open Tables line. The work was done by AI agents on a home computer and reviewed by a human before publication.

## What is in it

| | |
|---|---|
| Publications | 20 (Alice and Infoteca-e, Embrapa's open repositories), 1978 to 2023: 12 journal articles and 8 Embrapa bulletins |
| Trials | 61 (53 experiments and 8 joint analyses; 46 field, 13 greenhouse pots, 1 laboratory, 1 storage), in Piauí, Ceará, Maranhão, Pernambuco, Bahia, Sergipe, Alagoas, Pará, Roraima and Acre |
| Records | 2,541 (grain yield per area and per plant, disease score, incidence and reaction class, plant biomass, nodule number and mass, nitrogen fixation, pods per plant, grains per pod, pod length, 100-grain weight, grain protein, water absorption and other grain traits, water use, yield loss or gain, pest density, nematode counts and others) |

Files:
- `data/cowpea_trials.csv`: the dataset, one record per printed value, with `doc_id` and `trial_id`. Columns are described in `method/schema.json`. Where a record takes a value from its table column or from the whole table (unit, statistic, target, plant part, organism stage, factor level, class label, assessment time), the value is filled in and `inherited` says where it came from.
- `data/cowpea_trials_context.csv`: one row per trial (place, affiliation, season, sowing and harvest date, water regime, tillage system, previous crop, cultivar, pest or pathogen inoculation, rhizobium inoculation, application method and timing, sprays given to every plot, spacing or plant density, base fertilization, replicates, design). Join on `doc_id` + `trial_id`; an empty `application_stages` or `n_applications` in a record means the trial's value applies.
- `data/sources.csv`: the 20 publications, with authors, record link and licence notice.
- `qa/decisions.csv`: every disagreement between the two independent transcriptions and how it was settled against the PDF (3,627 decisions, with page).
- `method/`: the schema, the comparison script and the merge script.

## How it was made

1. **Collection.** An agent searched Embrapa's open repositories for publications with quantitative trial tables on cowpea (2,724 records after removing duplicates), read the record page and PDF of 58 and took 20, recording every candidate it did not take, with the reason.
2. **Two independent transcriptions.** Two agents per publication transcribed the trial context, the labels that apply to a whole table or to one column (which statistic, which test, what the letters mean, when the crop was assessed, which plant part, the unit and what it is counted per) and every table cell on the topic into a fixed schema, without seeing each other's work, copying numbers exactly as printed and accounting for every data cell.
3. **Comparison and adjudication.** A script paired the two transcriptions, trial by trial, table by table and record by record, and listed every disagreement and every value present in only one of them. Each one was settled by checking the PDF, with the page as evidence.

## How accurate it is

- **Numbers:** no number or significance letter was misread in either transcription, the fifth Open Tables round in a row with none. Of the 2,538 paired records, 2,536 matched as printed. The other 2 are not misread digits. silva2007 prints "3.4" with a point (checked at 600 dpi) and one transcription wrote "3,4"; the value is the same. In fazolin1986 the text on page 4 prints "73,%" with the decimal missing: one transcription wrote 73, the other marked it illegible, and the dataset keeps it as illegible with `value` empty (the table mean is 73.55).
- **Context and labels:** one transcription alone was fully correct on 83.0% and 81.9% of the 2,539 required records, counting the one record the second left out. Most errors came from one rule missed across a whole document. In three documents the assessment time is stated in the methods and one transcription did not carry it to the tables: barreto1999 (weekly readings, 630 fields in 274 records), fazolin1986 (end of the crop cycle, 297 fields in 94 records) and andrade2002 (end of the cycle, 203 fields in 77 records). In sousa2021 the packaging of the stored grain (vacuum or plain bag), which is the treatment, was entered as an application (146 fields, all 144 records). Without these four cascades, one transcription alone would be fully correct on 91.7% and 96.4% of records. Smaller ones: the per-plant basis of a unit given in the methods (fazolin1986, 56 fields) or in the caption (cardoso1997, 44), the assessment time of one column copied to another (santos1978, 64) and two unnumbered blocks of a table merged into Table 1 (cardoso1981, 45). The six cascades over 50 fields make up 1,396 of the 1,871 fields decided against one side (75%). One transcription also entered 6 values that are not data: 2 ratios worked out in the text of moraes1980 and 4 increments in the text of gualter2011 that its Table 2 does not support; the dataset keeps the table and flags the conflict. All 3,627 decisions were settled against the PDF, so the dataset does not depend on either transcription alone.
- **Known limits:** values shown only in charts without printed numbers were not read; no record comes from a figure and 77 come from the text. Powdery mildew is not covered: the two repositories have no trial table on it. Thrips and pod borers appear only in species or parasitism surveys, and the one sowing-date trial found (Rondônia, 1979) is a scan with a watermark on every page. No document comes from Tocantins or Mato Grosso; their candidates were stability analyses or too large. The 655 congress papers found in the search were not opened, and neither were the proceedings of the national cowpea congress (Conac). Five documents (moraes1980, fazolin1986, santos1978, cardoso1981, silva2007) are scans with a noisy text layer; their numbers were read from the rendered page, and the search for copied text and copyright notices is weaker on them. One document, cardoso1997 (plant density under irrigation in Teresina, PI), holds 355 records, 14.0% of the dataset, and barreto1999 and carvalho2016 hold 343 each; without cardoso1997, one transcription alone is fully correct on 84.4% and 81.2% of records. 674 records (26.5%) have no assessment time; `crop_stage_status` says whether the document does not print it (617) or it does not apply (57). An error made the same way in both transcriptions does not show in the comparison: the adjudicators found 9, and how many more there are has not been measured.

## Licence and citation

- The dataset (the CSV files, schema and scripts) is released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Please cite the original publications listed in `data/sources.csv` as well as this dataset.
- The publications are not redistributed. Embrapa's repositories show a CC BY-NC-ND 4.0 notice on every record page; it is the repository's notice, not a licence on the item. The 12 journal articles (3 in Pesquisa Agropecuária Brasileira, the others in Anais da Sociedade Entomológica do Brasil, Revista de Ciências Agroambientais, Revista Acadêmica: Ciências Agrárias e Ambientais, Revista Agro@mbiente On-line, Revista Agri-Environmental Sciences, Nematologia Brasileira, Scientia Agraria, Revista Brasileira de Engenharia Agrícola e Ambiental and Revista Conexão na Amazônia) keep their own terms, which were not checked. Two PDFs print a notice: barreto1999 prints "© Embrapa-CNPAT, 1999", and marsaro2011 prints the journal's note that the article is under a Creative Commons licence, without saying which. In the five noisy scans a notice could have been missed. Only numbers, which are facts, and short citations are used here.

Errors or missing trials: please [open an issue](https://github.com/paper-rerun/cowpea-trials-br/issues).

## How this dataset was made

This dataset was built by AI agents (Claude, by Anthropic) on a home computer and reviewed by a human before publication. No value was estimated or typed by hand: each one was transcribed from the source PDF twice, independently, and every disagreement was checked against the page. The method and scripts are in `method/`. How the wider project works: https://github.com/paper-rerun/paper-rerun/blob/main/METHOD.md

Contact: Filipe Tessaro, via issues on this repository.
