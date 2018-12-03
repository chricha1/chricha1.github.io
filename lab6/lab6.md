## Lab 6

#### Part 1

![alt text](https://chricha1.github.io/Fig3.PNG)
Figure 3: Donations – natural breaks map

![alt text](https://chricha1.github.io/Fig8and9.PNG)
(p<0.05) - Figure 8: Default significance map, Figure 9: Default cluster map

![alt text](https://chricha1.github.io/Fig11and12.PNG)
99999 permutations - Figure 11: Significance map, Figure 12: Cluster map

![alt text](https://chricha1.github.io/Fig20.PNG)
Figure 20: Cluster map (p<0.01)

![alt text](https://chricha1.github.io/Fig21.PNG)
Figure 21: Selected locations in significance map for p<0.01

![alt text](https://chricha1.github.io/Fig23.PNG)
Figure 23: Cluster map, Bonferroni (p<0.00012)

![alt text](https://chricha1.github.io/Fig27.PNG)
Figure 27: Cluster cores and neighbors (p<0.01)

![alt text](https://chricha1.github.io/Fig28.PNG)
Figure 28: Cluster cores and neighbors for p<0.01 overlaid on cluster map for p<0.05

![alt text](https://chricha1.github.io/Fig29.PNG)
Figure 29: Cluster cores and neighbors for p<0.01 in significance map

![alt text](https://chricha1.github.io/Fig31.PNG)
Figure 31: Conditional cluster map

![alt text](https://chricha1.github.io/Fig34.PNG)
Figure 34: Local Geary default significance map (p<0.05)

![alt text](https://chricha1.github.io/Fig35.PNG)
Figure 35: Local Geary default cluster map (p<0.05)

![alt text](https://chricha1.github.io/Fig36.PNG)
Figure 36: Local Geary high-high clusters

![alt text](https://chricha1.github.io/Fig37.PNG)
Figure 37: Local Geary low-low clusters

![alt text](https://chricha1.github.io/Fig38.PNG)
Figure 38: Local Geary negative spatial autocorrelation

![alt text](https://chricha1.github.io/Fig39.PNG)
Figure 39: Local Geary significance map (99999 permutations)

![alt text](https://chricha1.github.io/Fig40.PNG)
Figure 40: Local Geary (p < 0.01)

![alt text](https://chricha1.github.io/Fig41.PNG)
Figure 41: Local Geary FDR (p < 0.00012)

![alt text](https://chricha1.github.io/Fig45.PNG)
Figure 45: Gi statistic default significance map (999 permutations)

![alt text](https://chricha1.github.io/Fig46.PNG)
Figure 46: Gi statistic default cluster map (999 permutations)

![alt text](https://chricha1.github.io/Fig47.PNG)
Figure 47: Gi* statistic default cluster map (999 permutations)

![alt text](https://chricha1.github.io/Fig48.PNG)
Figure 48: Gi statistic significance map (99999 permutations)

![alt text](https://chricha1.github.io/Fig49.PNG)
Figure 49: Gi statistic cluster map (p < 0.01)

![alt text](https://chricha1.github.io/Fig50.PNG)
Figure 50: Gi statistic cluster map (FDR)


#### Part 2

1 . Created a Queen contiguity weight based on the ID variable
"OBJECTID" (instead of "CSA2010" because it is a string) in the
"Vital_Signs_16_Arts_and_Culture" shapefile.

![alt text](https://chricha1.github.io/Fig2-1.PNG)

2 . Ran a regression report to observe the correlation between
"cebus16" (Number of Businesses that are Arts-Related
per 1000 Residents) and "libcard16" (Number of Persons with
Library Cards per 1,000 Residents).

I compared the probability of Lagrange Multiplier (lag)
with the probability of Lagrange Multiplier (error). Both were
significant (p < 0.05), but LM (error) was more significant
than LM (lag).

![alt text](https://chricha1.github.io/Part2Fig2.PNG)

I found that the Moran's I was a positive number so that means
there is a correlation between the number of persons with library cards
and the number of art-related businesses.

3 . Created the Bivariate Local Moran's I map.

![alt text](https://chricha1.github.io/Part2Fig3.PNG)

The high-high (dark red) Downtown, Mount Vernon, and Charles Village neighborhoods
are bordered by neighborhoods with low numbers that are not significant enough
to cluster and split into low and high numbers when compared with the
rest of Baltimore City.

The low-high (light blue) neighborhoods have low numbers but are bordered by
neighborhoods with high numbers.

#### Part 3

Aggregating arts and culture data (such as arts-related
businesses, employment in arts-related businesses,
and public library membership) is necessary to identify
and promote the health of artists, arts organizations, and,
as a result, communities as a whole.

In creative placemaking, partners from public,
private, non-profit, and community sectors strategically shape
the physical and social character of a neighborhood, town, city,
or region around arts and cultural activities.

Creative placemaking animates public and private spaces,
rejuvenates structures and streetscapes, improves local
business viability and public safety, and brings diverse
people together to celebrate, inspire, and be inspired. Therefore,
creative placemaking impacts the well-being of Baltimore residents.
