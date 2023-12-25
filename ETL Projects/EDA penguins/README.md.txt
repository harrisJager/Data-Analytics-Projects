# EDA Penguin Dataset

**Author:** Harris Rizwan  
**Date:** 2023-12-19  
**Output:** html_document


The provided R code conducts Exploratory Data Analysis (EDA) on a penguin dataset. The analysis is structured into different exercises, each addressing specific aspects of the dataset. Here's a summary of what the code does:

Loading Data:

Reads a CSV file containing penguin data into a data frame (df1).
Displays the first few rows of the dataset using head(df1).
Basic Information:

Checks the number of observations and variables using ncol(df1) and names(df1), respectively.
Generates a detailed summary of the dataset using the describe function from the psych package.
Species and Gender Analysis:

Counts the number of penguins per species and per species-gender combination.
Computes summary statistics, including minimum, median, mean, and maximum body mass for each species and gender.
Quantitative Statistics:

Calculates additional quantitative statistics, such as mean culmen length, culmen depth, flipper length, and body mass for each species and gender.
Visualizations:

Creates a pairs plot for numerical variables.
Generates histograms, density plots, boxplots, and scatterplots to visualize the distribution and relationships among variables, considering species, gender, and island factors.
Produces an interactive scatterplot using ggplotly.
The code is designed for an in-depth exploration of the penguin dataset, providing both numerical summaries and visualizations to gain insights into the distribution and relationships among variables. The analyses are organized into exercises, making it easy to follow and understand the exploratory process. Users can adapt the file paths as needed and execute the code in their R environment for a comprehensive analysis of the penguin dataset.



## Prerequisites

Before running the code, make sure to install the required R packages:

```R
install.packages("ggplot2")
install.packages("GGally")
install.packages("dplyr")
install.packages("plotly")
install.packages("psych")
install.packages("doBy")
Then, load the necessary libraries:


library(ggplot2)
library(GGally)
library(dplyr)
library(plotly)
library(psych)
library(doBy)
Loading Data
R


Read the CSV file into a data frame:

R
# Read CSV file into a data frame
df1 <- read.csv2("YourDirectory\\PenguinsWithoutMissingValues.csv")
head(df1)
Exercise 1: How many observations do we have? How many variables?
R

# Number of columns
num_columns <- ncol(df1)
num_columns
Exercise 2: What are the names of the observed variables?
R

# Variable names
variable_names <- names(df1)
variable_names
Exercise 3: Provide a summary statistics of the columns?
R

# Detailed summary statistics
detailed_summary <- describe(df1)
detailed_summary
Exercise 4: How many penguins per Species are there?
R

# Penguins per species
penguins_per_species <- table(df1$Species)
penguins_per_species
Exercise 5: How many penguins per Species and Gender are there?
R

# Penguins per species and gender
penguins_count <- df1 %>%
  group_by(Species, Gender) %>%
  summarize(Count = n())
penguins_count
Exercise 6: Show BodyMass_g statistics per Species and Gender?
R

# BodyMass_g statistics
summary_table <- df1 %>%
  group_by(Species, Gender) %>%
  summarize(
    Number_of_Observations = n(),
    Min_BodyMass = min(BodyMass_g),
    Median_BodyMass = median(BodyMass_g),
    Mean_BodyMass = mean(BodyMass_g),
    Max_BodyMass = max(BodyMass_g)
  )
summary_table
Exercise 7: Quantitative statistics per Species and Gender?
R

# Quantitative statistics
statistics_table <- df1 %>%
  group_by(Species, Gender) %>%
  summarize(
    Number_of_Observations = n(),
    Mean_CulmenLength_mm = mean(CulmenLength_mm),
    Mean_CulmenDepth_mm = mean(CulmenDepth_mm),
    Mean_FlipperLength_mm = mean(FlipperLength_mm),
    Mean_BodyMass_g = mean(BodyMass_g)
  )
print(statistics_table)
Exercise 8: Pairs plot for numerical variables
R

# Pairs plot
ggpairs(numerical_vars)
Exercise 9: Histograms for CulmenLength_mm
R

# Histograms
ggplot(df1, aes(x = CulmenLength_mm, fill = Species)) +
  geom_histogram(binwidth = 1, color = "black", position = "identity", alpha = 0.7) +
  labs(title = "Histogram by Species", x = "Culmen Length (mm)", y = "Frequency") +
  scale_fill_manual(values = c("Adelie" = "skyblue", "Chinstrap" = "lightgreen", "Gentoo" = "salmon"))
Exercise 10: Density plot for CulmenLength_mm
R

# Density plot
ggplot(df1, aes(x = CulmenLength_mm, fill = Species)) +
  geom_density(alpha = 0.5) +
  facet_grid(Gender ~ .) +
  labs(title = "Density plot for CulmenLength_mm by Species (facet_grid: Gender)",
       x = "CulmenLength_mm",
       y = "Density")
Exercise 11: Boxplot for CulmenLength_mm
R

# Boxplot
ggplot(df1, aes(x = "", y = CulmenLength_mm, fill = Species)) +
  geom_boxplot() +
  facet_grid(Gender ~ .) +
  labs(title = "Boxplot for CulmenLength_mm (facet_grid: Gender, colored by Species)",
       x = "",
       y = "CulmenLength_mm")
Exercise 12: Scatterplot for CulmenLength_mm and BodyMass_g
R

# Scatterplot
ggplot(df1, aes(x = CulmenLength_mm, y = BodyMass_g, color = Species)) +
  geom_point() +
  facet_grid(Gender ~ .) +
  labs(title = "Scatterplot for CulmenLength_mm and BodyMass_g (facet_grid: Gender, colored by Species)",
       x = "CulmenLength_mm",
       y = "BodyMass_g")
Exercise 13: Interactive Scatterplot with ggplotly
R

# Interactive Scatterplot
gg_scatterplot <- ggplot(df1, aes(x = CulmenLength_mm, y = BodyMass_g, color = Species, text = IndividualID)) +
  geom_point() +
  facet_grid(Gender ~ .) +
  labs(title = "Interactive Scatterplot with ggplotly (facet_grid: Gender, colored by Species)",
       x = "CulmenLength_mm",
       y = "BodyMass_g")

# Convert ggplot to ggplotly
ggplotly(gg_scatterplot, tooltip = "text")
Feel free to run these code snippets in your R environment, and make sure to adapt file paths if needed.