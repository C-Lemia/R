
# R
#Meus estudos com a linguagem R.

#Treinando Big Data - Data Science Academy.

setwd("C:/FCD")
getwd()

# Dataset: Berkeley Earth.


# Instalando Pacotes:
install.packages("readr")

install.packages("data.table")

install.packages("dplyr")

install.packages("ggplot2")

library(readr)

library(data.table)

library(dplyr)

library(ggplot2)

# Lendo CSV com fread.

system.time(df <- fread("TemperaturasGlobais.csv"))

View(df)

# Criando dados carregados:

citychina <- subset(df,Country == 'China') # Amostra de dados cidades da China.
citychina <- na.omit(citychina) # Omite qualquer valor em branco.
head(citychina) # visualiza os dados.
View(citychina)# visualizar os dados em tabela.
nrow(df) # # numeros de linhas.
nrow(citychina) # numeros de linha com dados da China.
dim(citychina)# Dimensoes da tabela.


# Convertendo Datas da Tabela.
citychina$dt <- as.POSIXct(citychina$dt,format = '%Y-%m-%d') #Conversao formato data.
citychina$Month <- month(citychina$dt)# extrair o mes.
citychina$Year <- year(citychina$dt) # extrair o ano.
View(citychina)

# Carregando subsets de algumas cidades

# Rongcheng

rong <- subset(citychina,City == "Rongcheng") 
rong <- subset(rong,Year %in% c(1976,1846,1896,1946,1996,2012)) # listas de anos - vetor - para analise


# Yichun

yic <- subset(citychina,City == "Yichun")
yic <- subset(yic,Year %in% c(1976,1846,1896,1946,1996,2012))

# Yidu

yid <- subset(citychina,City == "Yidu")
yid <- subset(yid,Year %in% c(1976,1846,1896,1946,1996,2012))


# Plots

p_yic <- ggplot(yic,aes(x = (Month), y =AverageTemperature, color = as.factor(Year))) +
  geom_smooth(se = FALSE, fill = NA, size = 2) +
  theme_light(base_size = 20) +
  xlab('Mes') +
  ylab("Temperatura Media") +
  scale_color_discrete("") +
  ggtitle("Temperatura Media ao Longo dos Anos em Yichun")+
  theme(plot.title = element_text(size = 18))

#######

p_rong <- ggplot(rong,aes(x = (Month), y =AverageTemperature, color = as.factor(Year))) +
    geom_smooth(se = FALSE, fill = NA, size = 2) +
    theme_light(base_size = 20) +
    xlab('Mes') +
    ylab("Temperatura Media") +
    scale_color_discrete("") +
    ggtitle("Temperatura Media ao Longo dos Anos em Rongcheng")+
    theme(plot.title = element_text(size = 18))
  
#####
  
p_yid <- ggplot(yid,aes(x = (Month), y =AverageTemperature, color = as.factor(Year))) +
    geom_smooth(se = FALSE, fill = NA, size = 2) +
    theme_light(base_size = 20) +
    xlab('Mes') +
    ylab("Temperatura Media") +
    scale_color_discrete("") +
    ggtitle("Temperatura Media ao Longo dos Anos em Yidu")+
    theme(plot.title = element_text(size = 18))

# Plotando:

p_rong
p_yic
p_yid
