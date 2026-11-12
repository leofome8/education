# Paying for Learning: Brazil's results-based education transfers

Replication materials for *Paying for Learning: What the First Years of Brazil's Results-Based Education Transfers Can and Cannot Tell Us*.

The paper studies two results-based channels created by Brazil's 2020 Fundeb reform: the state ICMS-Educacional laws, which distribute part of the municipal value-added tax quota by learning results, and the federal VAAR learning grant. It uses three designs: a regression discontinuity at the VAAR learning cutoff (main design), a staggered difference-in-differences across states (complementary design) and a within-state exposure design with a national placebo (diagnostic).

## Repository layout

| Folder | Contents |
|---|---|
| `notebooks/` | Google Colab notebooks that download the public data, build the panels and produce the results. Code cells are hidden behind forms; outputs are HTML tables. |
| `scripts/` | Short Python scripts that reproduce the main tables from the derived data, without Colab. |
| `src/` | Shared code of notebook 01 (Callaway and Sant'Anna estimator), used by the scripts. |
| `data/derived/` | Derived data sets built by the notebooks from public sources. |
| `results/` | Result files behind each table of the paper. |

## Notebooks

| Notebook | What it does | Paper |
|---|---|---|
| `01_icms_educacional_ideb_cs_v3.ipynb` | Ideb/Saeb municipal panel, treatment timing of 26 state laws, Callaway and Sant'Anna estimates, bootstrap, permutation, cohort and leave-one-state-out results | Tables 2, 2b, A1, A3, A4 |
| `03_icms_municipal_extracao_v5.ipynb` | Reads the official ICMS annexes (PDF, XLS) of Bahia, Piauí, Paraná and Rondônia and builds the municipal panel of education indices, with validation checks | Table A2, Section 4 |
| `04_vaar_regressao_descontinua_v3.ipynb` | VAAR files 2023 to 2026, first stage in reais, sharp and fuzzy regression discontinuity, validity tests, sensitivity | Tables 3a, 3b, A5, A6, A7 |
| `05_intensidade_icms_ideb_v2.ipynb` | Money at stake under the state rule (Siconfi DCA 2019), within-state design, event study, national placebo | Tables 4, A8, A9 |
| `06_mecanismos_vaar_contas_v0.ipynb` | Municipal accounts 2022 to 2025 (Siconfi) around the VAAR cutoff, spending and pass-through | Table 5 |
| `07_did_pandemia_v0.ipynb` | State design with comparison cells matched on the 2019 to 2021 pandemic shock, relative-magnitudes sensitivity | Tables 2c, A10 |

Run each notebook in Colab with *Runtime > Run all*. Parameters are in the form of cell 0. Downloads are cached in Google Drive (`MyDrive/artigo_a1_dados_inep`, `MyDrive/artigo_a1_dados_icms`). When INEP blocks downloads from Colab servers, the notebooks fall back to Base dos Dados (BigQuery) or to a manual upload. With 999 bootstrap draws and 999 permutations, notebooks 01 and 07 take from several minutes to about two hours.

## Scripts

From the `scripts/` folder:

```
pip install -r ../requirements.txt
python state_did_support.py 999   # Table 2: main state-level estimates (about 30 to 40 minutes with 999)
python state_did_sensitivity.py   # Table 2c
python rd_equivalence.py          # Table 3d
python rd_heterogeneity.py        # Table 3c, interactions with a common bandwidth, pandemic balance at the cutoff
```

## Data

All raw data are public:

* INEP: Ideb and Saeb municipal results (2005 to 2025) and the VAAR files of the 2023 to 2026 rounds.
* Tesouro Nacional, Siconfi: municipal annual accounts (DCA, annexes I-C and I-E), 2019 and 2022 to 2025.
* State governments and audit courts: ICMS participation indices (SEC-BA, TCE-PI, Governo do Paraná, SEFIN-RO), listed in Table A2 of the paper.
* IBGE: municipality codes and names.

Derived files in `data/derived/`:

| File | Description |
|---|---|
| `base_tratamento_icms.csv` | State laws: law, education weight, law year, first payment year, state test, equity term |
| `painel_icms_educacional.csv` | Municipal education indices extracted from the official annexes (3,190 municipality-year rows) |
| `painel_ideb_anos_iniciais_municipal.csv` | Municipal panel of early-grade Saeb scores with treatment cohort |
| `siconfi_2019.csv`, `exposicao_por_municipio.csv` | 2019 accounts and money at stake for the within-state design |
| `rd_amostra_2023.csv`, `rd_amostra_2025.csv` | VAAR networks with running variable, grants in reais and scores |
| `rd_amostra_contas.csv` | Networks within 0.15 of the 2023 cutoff linked to their 2022 to 2025 accounts |
| `queda_pandemia_por_municipio.csv` | Change in early-grade score between 2019 and 2021 by municipality |

## Units

Scores are Saeb standardized mean scores (0 to 10 scale). Effects in standard deviations divide by the 2019 cross-municipality standard deviation: 0.84 points for the early grades and 0.65 for the final grades.

## License

Code: MIT License (see `LICENSE`). Derived data: CC BY 4.0, with credit to the original public sources above.

## Citation

Forero Mendoza, L. A. (2026). Paying for Learning: What the First Years of Brazil's Results-Based Education Transfers Can and Cannot Tell Us. Working paper.
