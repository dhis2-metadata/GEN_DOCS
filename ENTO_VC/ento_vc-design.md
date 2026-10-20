# Entomology & Vector Control - System Design Guide { #ento-vc-design }

## Background and Purpose

The DHIS2 standard modules for **Entomology and Vector Control (E&VC)** have been developed to support countries to improve the collection and use of entomological and vector control interventions data to inform programmatic decisions.
All the modules have been designed in line with existing WHO recommendations, standard protocols and guidance. These modules complement already existing modules for [malaria epidemiology](#mal-agg-design). They contain a set of standard data collection forms and, depending on the module, automatically calculated indicators, data visualizations and thematic dashboards that allow to collect, visualize and interpret data from the following activities in line with WHO recommendations:

**Insecticide-treated nets (ITNs)**

- [ITN Mass Campaign](#vc-itn-mc-design)
- [ITN Bioefficacy Monitoring](#ento-itn-bio-design)

**Indoor residual spraying (IRS)**

- [IRS Mass Campaign](#vc-irs-campaign-design)
- [IRS Residual Efficacy Monitoring](#ento-irs-rem-design)

**Breeding sites monitoring**

- [Larviciding](#ento-bsm-larv-design)

**Insecticide resistance monitoring**

- [Integrated Vector Management - Discriminating Concentration Bioassay](#ento-ivm-dcb-design)

The WHO configuration packages consist of DHIS2 metadata that provide standard configurations of DHIS2 to support the collection of health data following WHO recommendations.

## System Design Overview

### Use Case

With these modules, countries can:

- **collect data** from the field, insectaries or laboratories, using mobile phones, tablets or computers, online and offline, and geolocated;
- **integrate entomological and vector control data** with epidemiological data and other types of relevant data (e.g. climatological data, stock data);
- **calculate standard** entomological and vector control indicators automatically and
- **develop custom visualizations** (tables, graphs and maps) and dashboards to inform specific needs.

### General Structure of the Activities

This chapter summarizes the published modules as of October 2026. It will be updated as more modules and packages are added to their respective E&VC activities.

<!-- TODO: update ento-vc-100-en.png to add the Insecticide resistance monitoring activity and the IVM Discriminating Concentration Bioassay module -->
![Entomology program structure](resources/images/ento-vc-100-en.png)

The diagram provides an overview (from darker to lighter green) of the **activities, modules, and packages** currently available in the DHIS2 for E&VC. Further use cases and descriptions are provided in the design guides of the modules.

### Rationale for Program Structure

Every standard method or procedure for the collection of entomological data and every vector control intervention is different and requires a different data collection process. For this reason, several modules have been developed, each to support a different entomological or vector control activity. Such a modular approach allows countries to choose which modules to implement, depending on their national needs.

Entomological data is often collected through bioassays or mosquito collections that are repeated several times for the same place and time period (e.g. multiple WHO cone bioassays for the monitoring of IRS efficacy can be conducted on the same day in different houses, several traps can be placed on the same night in different houses of a village to collect mosquitoes, several susceptibility bioassays can be run on mosquitoes collected from the same site). In addition, some vector control activities also require collecting data repeatedly for the same geographical and time period (e.g. indoor residual spraying in several houses in one area on the same day). Therefore, the entomology and vector control modules make use of both event and tracker programs to meet the needs of entomologists and vector control specialists in the field.

During implementation in countries, modules are adapted to country needs to facilitate their field data collection.

### Intended Users

These packages are intended to be used by:

- **Field entomologists** and personnel involved in the implementation of vector control interventions to collect data on entomology and vector control activities
- **Laboratory and insectary technicians** to enter results of bioassays and mosquito analysis
- Vector-borne disease **program managers and public health officers** to interpret the data collected and use such information during decision making processes.

## User Groups

Each module is distributed with its own three user groups (Admin, Access and Data capture), named after the module (e.g. *ENTO IVM - Admin*, *ENTO IVM - Access*, *ENTO IVM - Data capture* for the Discriminating Concentration Bioassay module). All modules follow the sharing matrix below.

| User group        | Dashboard         | Program Metadata  | Program data         |
|-------------------|-------------------|-------------------|----------------------|
| **Admin**         | Can edit and view | Can edit and view | No Access            |
| **Access**        | Can edit and view | Can view only     | Can view only        |
| **Data capture**  | No access         | Can view only     | Can capture and view |

The Dashboard column applies only to modules that include dashboards.

## Android Compatibility

DHIS2 configuration packages are also compatible with the DHIS2 Android Capture App, free to download on the Google Play store. Key considerations in design were to ensure that all forms are configured with sections that structure form layout for better display on Android devices. Also, with the requirement of minimal data disaggregation in these packages, all the dataset layouts should provide a concise view for Android display. Where a module uses long option lists (e.g. vector species or insecticide concentrations), these lists should be reduced to the values used nationally before deployment on mobile devices.

## Data Triangulation - Entomology and Malaria

The data collected in the entomology and vector control programs can be triangulated with the [malaria surveillance tracker for the follow up of foci](#mal-cs-design). In addition, the data from entomology and vector control programs can be jointly analyzed with the epidemiological data collected through the malaria surveillance tracker for the follow up of foci, the health-facility malaria aggregate package or the CHIS package for malaria to gain a better understanding of disease transmission dynamics, to identify priority areas for vector control interventions, to understand the effectiveness of vector control interventions and to investigate outbreaks or unexpected changes in disease burden. The entomological and vector control packages should be used jointly for better results. For example, data from the [IRS](#vc-irs-campaign-design) implementation packages should be interpreted together with data from the [IRS residual efficacy](#ento-irs-rem-design) package to understand the potential effectiveness of this intervention, as well as to plan future IRS campaigns.

Similarly, data from the [Discriminating Concentration Bioassay](#ento-ivm-dcb-design) module should be interpreted together with data on the insecticides deployed and their measured bioefficacy in the same geography ([ITN bioefficacy](#ento-itn-bio-design) and [IRS residual efficacy](#ento-irs-rem-design)): a fall in observed bioefficacy may reflect either the decay of the insecticide on the substrate or the resistance of the local vector population, and only the combination of the two data sources distinguishes them. Susceptibility results also inform the choice of insecticides for future ITN and IRS campaigns. Intensity, synergist and molecular or biochemical assays are not covered by a published module; where available, their results should be considered alongside discriminating concentration results to characterise resistance in an area.

![When to use MAL-Foci and the entomology modules](resources/images/ento-vc-002-en.png)

Other examples of possible data triangulations are the triangulation with numbers used to analyze in more depth either facility-based data like the information reported via the [malaria aggregate](#mal-agg-design) packages, or community-based data via the [CHIS package](#chis-agg-design) for [malaria](#chis-agg-mal-design), [integrated community case management](#chis-agg-iccm-design) or [community-based surveillance](#chis-agg-cbs-design).

## Further resources

DHIS2, in collaboration with the WHO, organized a [webinar](https://youtu.be/9NwZPWGkNsU) to explain and outline the use cases for the use of the "Breeding sites", "ITN - Bioefficacy" and "IRS - Residual efficacy" packages. The webinar also provides insights on the use of the malaria foci vs entomology modules.

The use case, configuration and implementation considerations of the insecticide resistance monitoring module are described in the [Discriminating Concentration Bioassay design guide](#ento-ivm-dcb-design). WHO lists the DHIS2 tools for vector control data collection and collation on its [vector control page](https://www.who.int/teams/global-malaria-programme/prevention/vector-control/dhis-data-collection-and-collation-tools).
