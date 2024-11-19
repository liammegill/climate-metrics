# Investigating suitable climate metrics for use in aviation

_Publication_: Alternative climate metrics to the Global Warming Potential are more suitable for assessing aviation non-CO2 effects

_Authors_:

- Liam Megill (1, 2), https://orcid.org/0000-0002-4199-6962   
- Kathrin Deck (2)  
- Volker Grewe (1, 2), https://orcid.org/0000-0002-8012-6783  

_Affiliation (1)_: Deutsches Zentrum für Luft- und Raumfahrt (DLR), Institut für Physik der Atmosphäre, Oberpfaffenhofen, Germany

_Affiliation (2)_: Delft University of Technology (TU Delft), Faculty of Aerospace Engineering, Section Aircraft Noise and Climate Effects (ANCE), Delft, The Netherlands

_Corresponding author_: Liam Megill, liam.megill@dlr.de

_doi_: https://doi.org/10.1038/s43247-024-01423-6

_data doi_: https://doi.org/10.4121/344e24ad-b2f5-4ed9-8d49-6efa2081d30c

---

## General introduction
You can download the code for this project at [4TU.ResearchData](https://doi.org/10.4121/344e24ad-b2f5-4ed9-8d49-6efa2081d30c). This dataset contains all data and code developed during research towards the linked article. It contains all elements required to reproduce the linked figures and analysis. The research was started in an MSc thesis by Liam Megill at the TU Delft ("Analysis of Climate Metrics for Aviation", http://resolver.tudelft.nl/uuid:9e84ee4d-af69-4550-8938-2ccf4caccb8c) and finished during his PhD project at the DLR.

---

## Description of the data

The data in the "data" folder was calculated using AirClim version 2.1 (Dahlmann et al., 2016). AirClim is confidential proprietary code of the DLR and cannot be made available to the public or readers without restrictions. Licensing of the code to third parties is conditioned upon the prior conclusion of a licensing agreement with the DLR. Qualified researchers can request an agreement on reasonable request from the corresponding author.

### GEN

In the `GEN` directory, the AirClim results for all simple emission profiles are provided. These are:
- *_2020 (P - pulse emission in the year 2020; C - constant emission from the year 2020 onwards; F - fleet emission starting in the year 2020)
- INC\* (percentage increasing emission - 0.5%, 0.8%, 1%, 6%, 7%).

These results are used by the `relative_metric_analysis.ipynb` notebook to analyse the general response of the Global Warming Potential (GWP), "Effective" Global Warming Potential (EGWP), Global Temperature Change Potential (GTP) and Average Temperature Response (ATR) with respect to the time horizon. Specifically, the results are used to create Figure 4 and Extended Data Figures 3, 4, 5, 6 in the linked article.

### CO2eq

In the `CO2eq` (CO2-equivalent) directory, the AirClim results for all full aviation scenario emission profiles are provided. These are:
- CORSIA: CORSIA scenario of Grewe et al. (2021), extended by 0.5% annual growth rate from 2100 until 2200
- COVID15s: COVID15s scenario of Grewe et al. (2021), extended by 0.5% annual growth rate from 2100 until 2200
- CurTec: CurTec scenario of Grewe et al. (2021), extended by 0.8% annual growth rate from 2100 until 2200
- Fa1: Fa1 scenario of IPCC (1999), extended by 0.8% annual growth rate from 2100 until 2200
- FP2050: FP2050 scenario of Grewe et al. (2021), extended by 0.5% annual growth rate from 2100 until 2200

These results are used by the `co2eq_analysis.ipynb` notebook to analyse the temporal stability (REQ 2) of climate metrics using CO2-eq trajectories and the resulting CO2 multipliers. Specifically, Figure 2 and Extended Data Figure 2 of the linked paper are created.

### MVMC

In the `MVMC` (*M*ulti*V*ariate *M*onte *C*arlo) directory, the AirClim results for the aircraft fleets in the Monte Carlo simulation are provided. A total of 10.000 fleets were analysed, split into 10 batches of 1000 fleets due to memory limitations. Fleets 1 to 3 are the reference low, medium and high fleet scenarios. The parameters defining each fleet are provided in `MVMC_init.txt`. These are:

- Idx: Index of fleet (within each batch)
- Year: Year in of fleet introduction
- Burn: Fuel burn factor. This describes the portion of the aircraft category this particular fleet encompasses. The reference fleet (Fleet 1) approximates the Airbus A320 (40% of DLR WeCare (Grewe et al., 2017) Category 4 - between 152 and 201 seats)
- NOx, Alt, Dist, CO2, H2O: Factors for NOx emissions, altitude, distance flown, CO2 and H2O emissions compared to the reference (Fleet 1)
- SSP: Background Shared Socio-economic Pathway (SSP, Meinshausen et al., 2020). 1-5 correspond to SSP1-1.9, SSP2-4.5, SSP3-7.0, SSP4-6.0, SSP8-5.0 respectively.
- Fuel: Fuel used. 1-3 correspond to conventional kerosene, Sustainable Aviation Fuel (SAF), hydrogen combustion and hydrogen fuel cells respectively.

The `multivariate_fleet_analysis.ipynb` notebook analyses the neutrality of the climate metrics with respect to aviation emissions (REQ 1) in the linked paper and creates Figure 1 and Extended Data Figure 1. The `gwps_analysis.ipynb` notebook uses batch_1/Fleet1 to produce Figure 3 of the linked paper, showing the CO2eq emissions calculated using the climate metric GWP* over time, demonstrating the flow-based nature of the GWP*.

---

## Data and code organisation and naming

You can download the code for this project at [4TU.ResearchData](https://doi.org/10.4121/344e24ad-b2f5-4ed9-8d49-6efa2081d30c). To view and use the code and data, unzip `dataset.zip` into the main directory with this readme file. The data is then provided in `data.zip`, which should be unzipped to a folder `data` within the main directory. The data corresponding to each notebook is explained in more detail in the notebook. Plots can be printed to `.png` files by uncommenting the instructions to define the png file name (`fig_savename` variable) and the `fig.savefig()` call in the plotting cells of the notebooks. Be aware that an `images` directory must be present. Otherwise change the path specified in the `fig_savename` variable. Example figures can be foud in the `images` folder once unzipped.

The structure of the `data/` directory is the following:

```
.
|-- GEN
|   |-- <emission> (C2020, F2020, INC05, INC08, INC1, INC6, INC7, P2020)
|   |   |-- SSP* (SSP1-19, SSP2-45, SSP3-7, SSP4-6, SSP5-85)  
|   |       |-- AGWP100_2020_spec.txt
|   |       |-- *_emis.txt (for CO2, NOx)
|   |       |-- EI-NOx.txt
|   |       |-- RF_*_taumean_rfmean.txt (CH4, CO2, Cont, H2O, O3, PMO)
|   |       |-- dt_*_taumean_rfmean_lammean.txt (CH4, CO2, Cont, Ges, H2O, O3, PMO)
|   |-- E_bg_fuel_GEN.txt
|
|-- CO2eq
|   |-- <scenarios> (CORSIA, COVID15s, CurTec, FP2050, Fa1)
|   |   |-- SSP* (SSP1-19, SSP2-45, SSP3-7, SSP4-6, SSP5-85)
|   |       |-- AGWP100_2050_spec.txt
|   |       |-- *_emis.txt (for CO2, NOx)
|   |       |-- EI-NOx.txt
|   |       |-- RF_*_taumean_rfmean.txt (CH4, CO2, Cont, H2O, O3, PMO)
|   |       |-- dt_*_taumean_rfmean_lammean.txt (CH4, CO2, Cont, Ges, H2O, O3, PMO)
|   |-- E_bg_new_scen.txt
|
|-- MVMC
|   |-- batch_* (1 to 10)
|   |   |-- Fleet* (1 to 1003)
|   |   |   |-- AGWP100_*_spec.txt 
|   |   |   |-- *_emis.txt (for CO2, NOx)
|   |   |   |-- EI-NOx.txt
|   |   |   |-- RF_*_taumean_rfmean.txt (CH4, CO2, Cont, H2O, O3, PMO)
|   |   |   |-- dt_*_taumean_rfmean_lammean.txt (CH4, CO2, Cont, Ges, H2O, O3, PMO)
|   |   |-- MVMC_init.txt
|   |-- AGWPH_CO2_*.txt (SSP1-19, SSP2-45, SSP3-7, SSP4-6, SSP5-85)
|   |-- tot_err_arr_*.npy (av20, av50, av100, maxT)
|   |-- E_bg_fuel_MC.txt
|   |-- MVMC_init.py
|   |-- MVMC_init.txt
```

---

## Python requirements

Next to a regular python installation, only three packages are required:
- numpy  
- matplotlib  
- seaborn  

To run the Jupyter notebooks interactively, the package ipykernel is also necessary. The notebooks have been run using Python 3.10 (pip 23.2.1) and the following specific versions:
- numpy 1.25.2  
- matplotlib 3.7.2  
- pandas 2.0.3  
- seaborn 0.12.2  
- ipykernel 6.25.1

A python 3.10 installation can be created automatically using pip3 or conda and `requirements.txt`.

When using conda, create the environment with:

```
conda create --name <name_environment> python==3.10
conda activate <name_environment>
pip install -r requirements.txt
```

---

## License

All data files are licensed under a CC-BY 4.0 (see `LICENSE/CC-BY-4.0.txt` file). All Jupyter notebooks and the Python script (`.py`) are licensed under an Apache License v2.0 (see `LICENSE/Apache-License-v2.0.txt` file). 

---

## Copyright

Copyright © 2024 Liam Megill

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0. Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

---

## References

Megill, L., Deck, K., Grewe, V. Alternative climate metrics to the Global Warming Potential are more suitable for assessing aviation non-CO2 effects. _Communications Earth & Environment_. 5, 1 (2024). doi: https://doi.org/10.1038/s43247-024-01423-6

Dahlmann, K., Grewe, V., Frömming, C. & Burkhardt, U. Can we reliably assess climate mitigation option for air traffic scenarios despite large uncertainties in atmospheric processes? _Transportation Research Part D: Transport and Environment_. 46, 40-55 (2016). doi: https://doi.org/10.1016/j.trd.2016.03.006

Grewe, V. et al. Mitigating the climate impact from aviation: achievements and results of the DLR WeCare proejct. _Aerospace_. 4, 34 (2017). doi: https://doi.org/10.3390/aerospace4030034

Grewe, V. et al. Evaluating the climate impact of aviation emission scenarios towards the Paris agreement including COVID-19 effects. _Nature Communications_. 12, 1 (2021). doi: https://doi.org/10.1038/s41467-021-24091-y

Meinshausen et al. The shared socio-economic pathway (SSP) greenhouse gas concentrations and their extensions to 2500. _Geoscientific Model Development_. 13, 8 (2020). doi: https://doi.org/10.5194/gmd-13-3571-2020
