---
title: "Global Temperature Trends in a Warming World"
author: "Samuel Meads"
date: "(`r format(Sys.time(), '%d %B, %Y')`)"
output: 
  github_document: 
      toc: true
---

![](/Users/sm/Desktop/DataScience/APY313_S24/APY313_DataPractical_Final/Pictures/ClimateChange.jpg)

```{r}
# Import Libraries
library(tidyverse)
library(dplyr)
library(knitr)
library(ggplot2)
library("stringr")
library(tidyr)
```

# Introduction

The relationship between the escalating concentrations of greenhouse gases, specifically carbon dioxide (CO₂) and methane (CH₄), and the increases in global average temperatures support contemporary understanding of climate dynamics. This connection not only highlights the anthropogenic impacts on climate change but also serves as a critical point for scientific questions aimed at explaining the effects and potential mitigation strategies for global warming.

Historical and modern scientific efforts have greatly contributed to the understanding of this relationship. Eunice Foote and, later in the 19th century, John Tyndall, with their pioneering experiments, both proved the heat-trapping characteristics of CO₂, as part of the basic knowledge toward the greenhouse effect, which is necessary for modern-day climatic science (Armstrong et al., 2018). In the 20th century, scientists, including Mann et al. (1998), further attempted to provide an explanation for the dominant role of the gases in recent climate variability and to confirm the continual impact that had already been observed in earlier research by using paleoclimatic information to link changes in greenhouse gas concentrations with large-scale temperature patterns.
The most recent studies, for instance, Hansen et al. (2006) and Mann et al. (1998), have not only upheld the early findings with great analysis but have continued to argue out how these gases influence modern climatic patterns. Some of these include changes in SSTs and their link to key climate events such as the El Niño. His work, through the documentary, indeed underscores near effects of these gases and points out to the constant increase in the temperatures around the world, which is in line with past predictions and models that sought to establish the trajectory of climate change.

They increasingly report that the increase of world temperatures is very much related to rising sea levels—one of those things they are seeing more often in climate studies of recent years. Mitchell (1989) pointed out that the enhanced greenhouse gas concentrations have warmed not only the atmosphere but have also contributed to its thermal expansion, melting ice caps, which have emerged as major factors for the increased observed rise in sea levels over the past century.

Building on these foundational experiments and studies, the present research aims to delve deeper into the correlations and causal relationships between the increases in specific greenhouse gases with global temperature trends. Using context from these studies and modern technological and methodological advances, this piece of work contributes to having a more cohesive understanding of the mechanisms involved in climate change by potentially confirming or challenging past findings.


# Methods

## Research Question
My hypothesis is as follows: increases in atmospheric carbon dioxide and methane concentrations are significantly correlated with rises in global average temperature.

### Null Hypotheses
### Alternative Hypotheses

## Data Analyses

Since I am interested in the relationships between  

### Data

Data from NASA

```{r}
# Import data
co2_data <- read.csv('/Users/sm/Desktop/DataScience/APY313_S24/APY313_DataPractical_Final/Data/CarbonDioxide.csv')
methane_data <- read.csv('/Users/sm/Desktop/DataScience/APY313_S24/APY313_DataPractical_Final/Data/Methane.csv')
globtemp_data <- read.csv('/Users/sm/Desktop/DataScience/APY313_S24/APY313_DataPractical_Final/Data/GlobalTemp.csv')
sealevel_data <- read.csv('/Users/sm/Desktop/DataScience/APY313_S24/APY313_DataPractical_Final/Data/SeaLevel.csv')
```

```{r}

head(co2_data)
head(methane_data)
head(globtemp_data)
head(sealevel_data)
```

### Descriptive Statistics

### Exploratory Data Analysis

### Time Series Analysis 

### Correlation and Causation Analysis

### Regression Analysis

### Casual Inference

### Model Evaluation

### Statistical Testing

### Sensitivity and Scenario Analysis

```{r}
co2_annual <- co2_data %>%
  filter(Year >= 1984) %>%
  group_by(Year) %>%
  summarize(AnnualAverageCO2 = mean(Monthly.Average, na.rm = TRUE))

methane_annual <- methane_data %>%
  group_by(Year) %>%
  summarize(AnnualAverageMethane = mean(Mean, na.rm = TRUE))

temp_annual <- globtemp_data %>%
  filter(Year >= 1984) %>%
  select(Year, No_Smoothing) %>%
  rename(AnnualAverageTemp = No_Smoothing)
```

```{r}
combined_data <- merge(co2_annual, methane_annual, by = "Year")
combined_data <- merge(combined_data, temp_annual, by = "Year")
colnames(combined_data)
```

```{r}
# Time series plot for CO2 Levels
ggplot(data = combined_data, aes(x = Year, y = AnnualAverageCO2)) +
  geom_line(color = "blue") +
  ggtitle("CO2 Levels Over Time") +
  xlab("Year") +
  ylab("CO2 Levels (ppm)") +
  theme_minimal()
```

```{r}
# Time series plot for Global Temperature Anomalies
ggplot(data = combined_data, aes(x = Year, y = AnnualAverageTemp)) +
  geom_line(color = "red") +
  ggtitle("Global Temperature Anomalies Over Time") +
  xlab("Year") +
  ylab("Temperature Anomaly (°C)") +
  theme_minimal()
```

```{r}
# Time series plot for Methane Concentrations
ggplot(data = combined_data, aes(x = Year, y = AnnualAverageMethane)) +
  geom_line(color = "green") +
  ggtitle("Methane Concentrations Over Time") +
  xlab("Year") +
  ylab("Methane (ppb)") +
  theme_minimal()
```

```{r}
# Scatter plot for CO2 Levels vs. Global Temperature Anomalies
ggplot(data = combined_data, aes(x = AnnualAverageCO2, y = AnnualAverageTemp)) +
  geom_point(color = "blue") +
  ggtitle("CO2 Levels vs. Global Temp Anomalies") +
  xlab("CO2 Levels (ppm)") +
  ylab("Global Temp Anomaly (°C)") +
  theme_minimal()
```

```{r}
# Scatter plot for Methane Concentrations vs. Global Temperature Anomalies
ggplot(data = combined_data, aes(x = AnnualAverageMethane, y = AnnualAverageTemp)) +
  geom_point(color = "green") +
  ggtitle("Methane Concentrations vs. Global Temp Anomalies") +
  xlab("Methane (ppb)") +
  ylab("Global Temp Anomaly (°C)") +
  theme_minimal()
```

```{r}
# Linear regression of Global Temp Anomaly on CO2 Levels
lm_CO2 = lm(AnnualAverageTemp ~ AnnualAverageCO2, data = combined_data)
summary(lm_CO2)
```

```{r}
# Linear regression of Global Temp Anomaly on Methane levels
lm_Methane = lm(AnnualAverageTemp ~ AnnualAverageMethane, data = combined_data)
summary(lm_Methane)
```

# Results

# Conclusion

# References 

## Articles

Armstrong, Anne K., et al. CLIMATE CHANGE SCIENCE: The Facts. Communicating Climate Change: A Guide for Educators, Cornell University Press, 2018, pp. 7-20. JSTOR, http://www.jstor.org/stable/10.7591/j.ctv941wjn.5.

Hansen, James, et al. "Global Temperature Change." Proceedings of the National Academy of Sciences, vol. 103, no. 39, 26 Sept. 2006, pp. 14288–14293. PNAS, www.pnas.org/cgi/doi/10.1073/pnas.0606291103. 

Mann, Michael E., Raymond S. Bradley, and Malcolm K. Hughes. "Global-Scale Temperature Patterns and Climate Forcing Over the Past Six Centuries." Nature, vol. 392, 23 Apr. 1998, pp. 779-787, https://www.nature.com/articles/33859

Mitchell, J. F. B. "The 'Greenhouse' Effect and Climate Change." Rev. Geophys., vol. 27, no. 1, 1989, pp. 115-139, doi:10.1029/RG027i001p00115.

## Data

National Aeronautics and Space Administration. "Climate Change: Vital Signs of the Planet." NASA, n.d., https://science.nasa.gov/climate-change/.

## Pictures

"Electric Towers During Golden Hour." Pexels, uploaded by Pixabay, https://www.pexels.com/photo/electric-towers-during-golden-hour-221012/.


