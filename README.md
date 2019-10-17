---
title: "desafíoSpike"
author: "Mirelys Diaz"
date: "16/10/2019"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Desafío Spike

DataSet 

```{r}
data_caudal<-readr::read_csv("/home/mirefresa/desafio_spike_cuencas/caudal_extra.csv")
```

**Visualizar contenido de la data**

```{r data_caudal}
summary(data_caudal)
```

## Plots de precipitación, temperatura y caudal

a.Función con una estación 

```{r pressure, echo=FALSE}
plot(pressure)
```

**Libreria a utilizar**
```{r}
library(ggplot2)
library(tidyverse)
library(dplyr)
library(stats)
```
**Filtrar Codigo de estación**
```{r}
time_plot_una_estacion<-data_caudal%>%filter(codigo_estacion==5730005)
summary(time_plot_una_estacion)
```
**Ordenar Columna fecha de minima y fecha maxima**
```{r}
time_plot_una_estacion[desc(time_plot_una_estacion$fecha),]

```

**Plot de una estación**
```{r}
plot(x=time_plot_una_estacion$fecha,type='p',main="Codigo de Estación 5730005",col='#1f77b4',
     y=time_plot_una_estacion$caudal)
```
b. Ahora escribir una función que haga plots de varias columnas, para poder visualizar caudal, precipitación y temperatura al mismo tiempo.
```{r}
time_plot_varias<-group_by(time_plot_una_estacion,caudal,precip_promedio,temp_max_promedio)
summarise(time_plot_varias,mean(caudal),mean(precip_promedio),mean(temp_max_promedio))

```

```{r}
summary(time_plot_varias$caudal)
summary(time_plot_varias$precip_promedio)
summary(time_plot_varias$temp_max_promedio)
```

```{r}
data(time_plot_varias)
plot(time_plot_varias$caudal,time_plot_varias$precip_promedio)
lines(ksmooth(time_plot_varias$caudal,time_plot_varias$precip_promedio, "normal", bandwidth = 2),col=2)
lines(ksmooth(time_plot_varias$caudal,time_plot_varias$precip_promedio, "normal", bandwidth = 5),col=3)
```


