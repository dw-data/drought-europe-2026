Europe drought 2026
================

# Introduction

Fix leaks or ban pools: As European countries prepare for hotter, drier years to come, here’s what the data says about how to really save water.

*In this repository, you will find the methodology, data and code behind
the stories that came out of this analysis.*

**Read the full story here:** [English](https://www.dw.com/a-78577712)

**Story by:** [Kira
Schacht](https://www.dw.com/en/kira-schacht/person-46893544)

- `analysis.Rmd` is the main file that contains the R code for the
  analysis
- `data/...` contains the raw data files used in the analysis, as well
  as the output data

# Read Data

## eurostat

We use the following eurostat datasets:

- [env_wat_cat](https://ec.europa.eu/eurostat/databrowser/view/env_wat_cat/default/table?lang=en&category=env.env_wat.env_nwat):
  Water use by supply category and economical sector, latest 10 years
- [demo_gind](https://ec.europa.eu/eurostat/databrowser/view/demo_gind/default/table?lang=en):
  Annual average population, since 2000

## EEA data

In addition, the dataset [EEA: Water abstraction by economic sector,
2000-2023](https://www.eea.europa.eu/en/analysis/indicators/water-abstraction-by-source-and/water-abstraction-by-economic-sector?activeTab=658e2886-cfbf-4c2f-a603-061e1627a515)
offers more complete figures on water use by sector for 37 European
countries, including the 27 current EU member states.

We exported each country’s dataset as a csv file on August 26, 2026.

It contains water abstraction in million m3 of water per year by sector,
divided into:

- “Agriculture” (NACE Section A)
- “Manufacturing” (Section C)
- “Public water supply” (Section E)
- “Electricity cooling” (Section D)
- “Others” (contains “Mining and Quarrying”, “Construction”, Sections B
  and F)

The categories sum to the total water abstraction for each country.

# Analysis

## Water use per sector

### Calculate households share of public water supply

The dataset provided by the EEA does not include households as a
separate category, but the eurostat data does have separate household
water use available for some countries.

Where possible, we will extract the share of public water supply used by
households from the eurostat dataset for the latest available year and
apply it to the EEA data:

`EP_HH / TOTAL_HH = "Households" / "All NACE activities plus households"`

| geo |     share |
|:----|----------:|
| BE  | 0.6587650 |
| BG  | 0.6818229 |
| CZ  | 0.6848894 |
| DK  | 0.6498361 |
| DE  | 0.8893735 |
| EE  |        NA |
| EL  | 0.8562564 |
| ES  | 0.6792338 |
| HR  | 0.7062145 |
| IT  | 0.8128696 |
| CY  | 0.9122558 |
| LV  | 0.9736691 |
| LT  | 0.6960529 |
| LU  |        NA |
| HU  | 0.8222227 |
| MT  | 0.6826528 |
| NL  | 0.7039214 |
| AT  |        NA |
| PL  | 0.7744187 |
| PT  |        NA |
| RO  | 0.5593716 |
| SI  | 0.6591161 |
| SK  |        NA |
| SE  | 0.7067239 |
| NO  | 0.6791010 |
| CH  | 0.6257745 |
| BA  |        NA |
| ME  | 0.6841805 |
| MK  | 0.7392758 |
| GE  |        NA |
| AL  | 0.8948616 |
| RS  | 0.7171959 |
| TR  | 0.7425850 |
| UA  |        NA |
| XK  | 0.6779661 |

### Water use per sector for 2023

#### EU total

calculate shares for each sector across all eu countries

| var                 | values_pp |
|:--------------------|----------:|
| Agriculture         | 360.62833 |
| Electricity.cooling | 390.69899 |
| Manufacturing       | 154.28574 |
| Others              |  16.95702 |
| Public.water.supply | 248.06845 |

#### Per country

output see `data/processed/eea_countries.csv`

## Total possible water savings in the EU

The EEA report [Contributions of water saving to a climate resilient
Europe (ETC BE Report
2025/1)](www.eionet.europa.eu/etcs/etc-be/products/etc-be-products/etc-be-report-2025-1-contributions-of-water-saving-to-a-climate-resilient-europe)
analyzes potential water savings for EU countries in each sector.

See this table on page 10:

![](eea_report_savings.png)

We’ll use this table to calculate and chart the potential savings for
each sector in absolute terms:

| var                 | values_pp | percent_low | percent_high | saving_low | saving_high |
|:--------------------|----------:|------------:|-------------:|-----------:|------------:|
| Agriculture         | 360.62833 |        0.05 |         0.20 |   342.5969 |   288.50266 |
| Electricity.cooling | 390.69899 |        0.45 |         0.95 |   214.8844 |    19.53495 |
| Manufacturing       | 154.28574 |        0.30 |         0.50 |   108.0000 |    77.14287 |
| Others              |  16.95702 |          NA |           NA |         NA |          NA |
| Public.water.supply | 248.06845 |        0.20 |         0.50 |   198.4548 |   124.03423 |

\##Water use in the EU over time

output see `data/processed/eea_time.csv`
