# FiscalDataFellow
Khushi Jain's Assignment Submission for Fiscal Data Fellow

# Importing Data
#specifying the path

path <- "C:/Users/khush/OneDrive/Desktop/Everything/K/CivilDataLab/district_level_mapping_2017.csv"

#reading contents of csv file

Expenditure2017 <- read.csv(path)

#contents of the csv file

view (Expenditure2017)

#Cleaning the Data for School Education Expenditure
#the package we'll be needing
library(tidyverse)

# 1.

#For School Education Data in under Major Head = 2202, 2203, 2204, 2205, 800, 4202.
GeneralEducation <- Expenditure2017 %>% filter(Major.Head.Code  %in% c("2202", "2203", "2204", "2205", "800", "4202"))

#To have a dataset for department wise allocations
df <- GeneralEducation[c(2,5,6,12,15,19)]
DepartmentWiseAllocation <- df

#For General Measures of Analysis of Department Wise Allocations
summary(DepartmentWiseAllocation)

# 2.
#For share of capital expenditure, Major Head = 800, 4202
CapitalExpenditure <- GeneralEducation %>% filter(Major.Head.Code  %in% c("800", "4202"))

# 3.
#To calculate for per-capita expenditure, I will be exporting the General Education data in excel and then adjusting for population data.
#Using the 2011 census data for district population. 

path2 <- "C:/Users/khush/OneDrive/Desktop/Everything/K/CivilDataLab/PerCapitaExpenditure.csv"
PerCapitaExpenditure2017 <- read.csv(path2)
view (PerCapitaExpenditure2017)


# 4. 
#Table for Revenue Expenditure and Utilization of Allotted Funds 
df1 <- GeneralEducation %>% filter(Major.Head.Code  %in% c("2202", "2203", "2204", "2205", "800"))
df2 <- df1[c(2,20)]

#R provides an inbuilt option to view table in ascending or descending order in the table view.

#Table for Capital Expenditure and Utilization of Allotted Funds 
df3 <- GeneralEducation %>% filter(Major.Head.Code  %in% c("800", "4202"))
df4 <- df3[c(2,20)]
#R provides an inbuilt option to view table in ascending or descending order in the table view.


# Notes
#Revenue Heads: 2202, 2203, 2204, 2205, 800
#Capital: 4202, 800

#For Exporting Data in Excel
install.packages("writexl")
library("writexl")
write_xlsx(GeneralEducation,"path to store the Excel file\\file name.xlsx")
