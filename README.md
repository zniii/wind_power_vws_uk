<h1>Capacity-Weighted Geospatial Virtual Wind Station (GVWS)</h1>
<h2>Summary</h2>
A Data Science dissertation project that develops and validates a
Capacity-Weighted Geospatial Virtual Wind Station (GVWS) for aggregate UK
wind generation modelling and rolling 24-hour-ahead forecasting.

<h2>Problem</h2>
Aggregate UK wind generation is driven by weather across hundreds of
onshore and offshore wind farms.

Traditional national weather averages assume every location contributes
equally to generation, which may not accurately represent the actual UK
wind fleet.

This project investigates whether weighting meteorological observations
by installed wind capacity improves representation quality and forecasting
performance.

<h2>Data Sources</h2>
- NESO Aggregate Wind Generation
- ERA5 Atmospheric Reanalysis
- Renewable Energy Planning Database (REPD)

<h2>Methodology</h2>
<img width="464" height="963" alt="image" src="https://github.com/user-attachments/assets/17ec339a-f15f-400b-b380-c022b941d06f" />

<h2>Key Results</h2>
<table>
  <tr>
    <th>Representaiton</th>
    <th>R²</th>
  </tr>
  <tr>
    <th>UK Mean</th>
    <th>0.872</th>
  </tr>
  <tr>
    <th>Wind-Farm Mean</th>
    <th>0.907</th>
  </tr>
  <tr>
    <th>Weighted Wind-Farm Mean</th>
    <th>0.931</th>
  </tr>
</table>
