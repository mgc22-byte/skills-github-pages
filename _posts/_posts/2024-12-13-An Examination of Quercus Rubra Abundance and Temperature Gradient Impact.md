---
title: "An Examination of Quercus Rubra Abundance and Temperature Gradient Impact"
date: 2024-12-13
---
Introduction
Forest plays a critical role in global carbon storage, water regulation and biodiversity conservation. However, climate change is altering the composition and distribution of tree species, with profound implications forest ecosystems. Understanding how environmental gradients, particularly temperature, influence specific tree species can provide insights into these changes. 
This project will focus on Quercus rubra (northern red oak), a significant species in North America forests due to its ecological and economic value. By examining how temperature gradients affect its abundance and migration trends, this research aims to identify patterns that reveal the species’ responses to climate change. Using data from the Forest and Inventory and Analysis (FIA) program, we will analyze spatial and temporal trends to better understand the relationship between Quercus rubra and temperature variations. 

Research Question
How does the temperature gradient influence the abundance and distribution of Quercus rubra across different regions over time, and what are the ecological implications of these changes on forest ecosystems and biodiversity?

Background
Forests cover about 31% of the Earth's land area, providing vital ecosystem services. Climate change has accelerated in tree species distributions, with many species moving to higher latitudes or elevations in response to warming temperatures (Parmesan, 2006; Iverson et al., 2008). Previous studies have established temperature as a key driver of tree migration, but little research has specifically focused on how Quercus rubra responds to temperature changes across its range. Quercus rubra is a cornerstone species of temperate forests in North America, contributing to ecosystems stability and providing critical habitat and resources. Its response to temperature changes will likely have cascading effects on forest ecosystems. By analyzing FIA data, this study seeks to provide a detailed understanding of Quercus rubra’s relationship with temperature gradients contributing to sustainable forest management and conservation strategies.

Hypothesis
Regions experiencing warmer temperatures will exhibit a decline in Quercus rubra abundance. Quercus rubra will show a northward migration trend in response to rising temperatures.

Results
library(ggplot2) library(tidyverse) library(readr) library(dplyr)

fia_data <- readRDS("U:\Biogeography Classwork\FIA_tree_master1.RDS") 
names(fia_data) 
head(fia_data) 
nro <- fia_data %>% 
filter(COMMON_NAME == "northern red oak")

head(nro)

head(fia_data) 
names(fia_data)
unique(fia_data$COMMON_NAME)

"map different variables of northern red oak"

var1 <- nro %>% 
group_by(SPECIES, PLT_lat, PLT_lon) %>%
summarise(nro = n_distinct(nro))

var1

library(ggplot2)

ggplot(var1, aes(x= PLT_lon, y = PLT_lat, color = nro))+
geom_point(size = 0.9) + 
scale_color_gradient(low = "yellow", high = "blue") + 
labs(title = "Abundance", x = "Longitude", y = "Latitude")

Rplot

var2 <- nro %>% 
group_by(HT, LON, LAT, DIA)%>% 
summarise(nro = n_distinct(COMMON_NAME))

ggplot(var2, aes(x = HT, y = DIA, color = nro)) + 
geom_point(size = 0.9) + 
scale_color_gradient(low = "red", high = "green") + 
labs(title = "Quercus Rubra Variables", x = "Height", y = "Diameter") 

Rplot04- height ![Rplot04- height](https://github.com/user-attachments/assets/76f2cd58-e55e-4a78-a803-0c4e459ef3e7)


sweet_b <- fia_data %>% 
filter(COMMON_NAME == "sweet birch")

var4 <- sweet_b %>% 
group_by(LON, LAT, STATECD) %>% 
summarise(sweet_b = n_distinct(SPCD))

var4

ggplot(var4, aes(x = LON, y = LAT, color = sweet_b, nro)) + 
geom_point(size = 1) + 
scale_color_gradient(low = "grey", high = "black") + 
labs(title = "Sweet Birch", x = "Longitude", y = "Latitude")

Rplot04-sweet birch ![Rplot04-sweet birch](https://github.com/user-attachments/assets/01a6058e-3c9f-4cc7-9815-03d562262113)


library(ggplot2) 
library(tidyverse)

ggplot(nro = nro) + 
geom_sf(aes(fill = "species")) + 
scale_fill_viridis_c(option = "plasma", na.value = "grey") + 
theme_minimal() + 
labs(title = "Distribution of Quercus Rubra", fill = "Distribution")

ggplot() + 
geom_sf(data = nro, fill = "lightblue", color = "black") + 
geom_sf(data = sweet_b, fill = "yellow", color = "red", linetype = "solid") + 
theme_minimal() + 
labs(title = "Distribution of Quercus Rubra")

library(ggplot2) 
library(sf) 
library(tidyverse)

ggplot()+ 
geom_sf(aes(fill= TempMean),color = "lightblue", nro)+ 
geom_sf(fill = "lightblue", color = "red", nro)+ 
scale_fill_viridis_d(name = "Longitude")+ 
labs(title ="Distribution of Quercus Rubra", x = "longitude", y = "latitude")
