# Introduce
This is a Orgdb for Oryza sativa. 
The information is get from RAP-db. 
The keytypes contain GID(RAP id), MSU id, symbol id(RAP db symbol id, CGSNL symbol id, Oryzabase symbol id), simple description and GO
# Install
``` R
if (!requireNamespace("remotes", quietly = TRUE))
    install.packages("remotes")

remotes::install_github("Tanghuanglei/org.OsativaT10.eg.db")
```
# Manual
## load
``` R
library("org.OsativaT10.eg.db")
```
## Information
```R
# the information the Orgdb contain
keytypes(org.OsativaT10.eg.db)
# what the information or the id look like
head(keys(org.OsativaT10.eg.db,keytypes = "GID"))
```
## ID conversion
``` R
library("clusterProfiler")
GID2SYMBOL <- bitr(GID_list,fromType="GID",toType="SYMBOL",OrgDb=org.OsativaT10.eg.db)
```
#What's more
Sometimes when you use this orgdb to do the go enrich analysis, choose the ont="ALL", there may be a problem that will happen, some rows of the ONTOLOGY column are show the NA.  I don't know the reason, one way to deal with the problem is using the GO2ON.xlsx to make a correct result
``` R
go_result <- enrichGo(gene_list,OrgDb=org.OsativaT10.eg.db,keyType="GID",ont="ALL")
result <- go_result@result
library(xlsx)
GO2ON <- read.xlsx("the path you put the GO2ON.xlsx",1,header=TRUE)
result <- merge(result,GO2ON,by.x="ID",by.y="GO",all.x=TRUE)
go_result@result <- result
```
