# API_BCRP

´´´R

require(jsonlite)
require(ggplot2)
require(lubridate)
require(stringr)
library(foreign)
library(readxl)
library(tidyverse)
require(tidyr)
library(dplyr)
require(plyr)

rm(list = ls())
#Colocar el codigo del metadato
#puede ser varios

#Colocamos el codigo de PBI del BCRP
metadato <- "PM04863AA"
i= 1
url <-paste('https://estadisticas.bcrp.gob.pe/estadisticas/series/api/',metadato[i],'/json/1930/2020', sep="") 
# Descargamos el url indicado
tmp1  <- fromJSON(readLines(url, warn="F"))
# Cambiamos el formato de los datos y cambiamos el valor de las variables con missing values.
df <-as.data.frame(lapply(tmp1$periods, function(y) gsub("n.d.", "-99999.99", y))) 

# Colocamos nombre a las columnas
names(df) <- c("año","pbi")

#Formato
str(df)

df$pbi <- round(as.numeric(df$pbi),2)
df$año <- as.numeric(df$año)
str(df)

head(df)

´´´
