# class07QD
Ilyas Darif A16577084
2024-04-23

today we will start our multi part exploration of some key machine
learning methods. we will begin with clustering - finding groupings in
data and then dimensionallity reduction

## Clustering

lets start with “k-means” cluttering the main function in base R for the
is `means()`

``` r
#makeup up some data
hist( rnorm(100000, mean=3))
```

![](lab7bimm143_files/figure-commonmark/unnamed-chunk-1-1.png)

``` r
tmp <- c(rnorm(30, -3), rnorm(30, +3))

x <- cbind(x=tmp, y=rev(tmp))
x
```

                   x          y
     [1,] -2.4949403  3.8383635
     [2,] -2.4343880  3.0082750
     [3,] -3.2174309  2.7609620
     [4,] -4.7055724  2.3098603
     [5,] -0.2048879  1.0560779
     [6,] -3.8227219  0.7072544
     [7,] -2.8561189  2.1371244
     [8,] -1.2124229  1.5396678
     [9,] -4.1332225  3.5156439
    [10,] -3.1257130  4.6189414
    [11,] -4.0115068  3.3438281
    [12,] -3.9084297  2.1236443
    [13,] -2.9197486  2.3778161
    [14,] -3.5737116  3.7559423
    [15,] -3.1732710  2.7975373
    [16,] -4.0046284  2.6944894
    [17,] -3.5276675  2.5628886
    [18,] -1.8444863  1.8583611
    [19,] -2.6657613  1.4213275
    [20,] -2.2989582  4.1001242
    [21,] -1.6138378  3.0554539
    [22,] -5.1660209  4.8679268
    [23,] -2.1696661  2.1856389
    [24,] -1.7050782  5.1050722
    [25,] -1.1001648  3.8668135
    [26,] -3.1149909  2.7545639
    [27,] -2.1420837  3.5107054
    [28,] -2.0064975  2.2026297
    [29,] -2.4568012  2.1550131
    [30,] -3.8271755  3.0234162
    [31,]  3.0234162 -3.8271755
    [32,]  2.1550131 -2.4568012
    [33,]  2.2026297 -2.0064975
    [34,]  3.5107054 -2.1420837
    [35,]  2.7545639 -3.1149909
    [36,]  3.8668135 -1.1001648
    [37,]  5.1050722 -1.7050782
    [38,]  2.1856389 -2.1696661
    [39,]  4.8679268 -5.1660209
    [40,]  3.0554539 -1.6138378
    [41,]  4.1001242 -2.2989582
    [42,]  1.4213275 -2.6657613
    [43,]  1.8583611 -1.8444863
    [44,]  2.5628886 -3.5276675
    [45,]  2.6944894 -4.0046284
    [46,]  2.7975373 -3.1732710
    [47,]  3.7559423 -3.5737116
    [48,]  2.3778161 -2.9197486
    [49,]  2.1236443 -3.9084297
    [50,]  3.3438281 -4.0115068
    [51,]  4.6189414 -3.1257130
    [52,]  3.5156439 -4.1332225
    [53,]  1.5396678 -1.2124229
    [54,]  2.1371244 -2.8561189
    [55,]  0.7072544 -3.8227219
    [56,]  1.0560779 -0.2048879
    [57,]  2.3098603 -4.7055724
    [58,]  2.7609620 -3.2174309
    [59,]  3.0082750 -2.4343880
    [60,]  3.8383635 -2.4949403

``` r
plot(x)
```

![](lab7bimm143_files/figure-commonmark/unnamed-chunk-2-1.png)

now lets try out `kmeans()`

``` r
km <- kmeans(x, centers=2)
km
```

    K-means clustering with 2 clusters of sizes 30, 30

    Cluster means:
              x         y
    1 -2.847930  2.841845
    2  2.841845 -2.847930

    Clustering vector:
     [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2
    [39] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2

    Within cluster sum of squares by cluster:
    [1] 70.05854 70.05854
     (between_SS / total_SS =  87.4 %)

    Available components:

    [1] "cluster"      "centers"      "totss"        "withinss"     "tot.withinss"
    [6] "betweenss"    "size"         "iter"         "ifault"      

``` r
attributes(km)
```

    $names
    [1] "cluster"      "centers"      "totss"        "withinss"     "tot.withinss"
    [6] "betweenss"    "size"         "iter"         "ifault"      

    $class
    [1] "kmeans"

> Q1. how many points in each cluster?

``` r
km$size
```

    [1] 30 30

> Q2. what commponant of your result object details cluster
> assignment/membership

``` r
km$cluster
```

     [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2
    [39] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2

> Q3. what are centers/mean values of each cluster

``` r
km$centers
```

              x         y
    1 -2.847930  2.841845
    2  2.841845 -2.847930

> Q4. make a plot of your data showing your clustering results
> (groupings/clusters and cluster centers)

``` r
plot(x, col=c("red", "blue"))
```

![](lab7bimm143_files/figure-commonmark/unnamed-chunk-8-1.png)

``` r
plot(x, col=c(1,2))
```

![](lab7bimm143_files/figure-commonmark/unnamed-chunk-9-1.png)

``` r
plot(x, col=km$cluster)

points(km$centers, col="green", pch=15, cex=3)
```

![](lab7bimm143_files/figure-commonmark/unnamed-chunk-10-1.png)

> Q5. run `kmeans()` again and cluster in 4 groups and plot the results.

``` r
km4 <- kmeans(x, centers = 4)
plot(x, col=km4$cluster)
```

![](lab7bimm143_files/figure-commonmark/unnamed-chunk-11-1.png)

## hierarchial clustering

this form of clustering aims to reveal the structure in your data by
progessively grouping points into a ever smaller number of clusters

the maion function in base R for this called `chlust()` . this function
does not take our input data directly but wants a “distance matrix” that
details how (dis)similar our inout points are to each other

``` r
hc <- hclust( dist(x) )
hc
```


    Call:
    hclust(d = dist(x))

    Cluster method   : complete 
    Distance         : euclidean 
    Number of objects: 60 

the print out above is not useful (unlike that from kmeans) but there is
a useful `plot()` method

``` r
plot(hc)
abline(h=10, col="red")
```

![](lab7bimm143_files/figure-commonmark/unnamed-chunk-13-1.png)

to get my results (my cluster membership vector) i need to “cut” my tree
using the function `cutree()`

``` r
grps <- cutree(hc, h=10)
grps
```

     [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2
    [39] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2

``` r
plot(x, col=grps)
```

![](lab7bimm143_files/figure-commonmark/unnamed-chunk-15-1.png)

# Principal Component Analysis (PSA)

the goal of PCA is to reduce the dimensionality of a dataset down to
some smaller subset of new variables (called PCs) that are a useful
bases for further analysis, like visualization, clustering ect

> Q1.

``` r
url <- "https://tinyurl.com/UK-foods"
x <- read.csv(url, row.names = 1)
x
```

                        England Wales Scotland N.Ireland
    Cheese                  105   103      103        66
    Carcass_meat            245   227      242       267
    Other_meat              685   803      750       586
    Fish                    147   160      122        93
    Fats_and_oils           193   235      184       209
    Sugars                  156   175      147       139
    Fresh_potatoes          720   874      566      1033
    Fresh_Veg               253   265      171       143
    Other_Veg               488   570      418       355
    Processed_potatoes      198   203      220       187
    Processed_Veg           360   365      337       334
    Fresh_fruit            1102  1137      957       674
    Cereals                1472  1582     1462      1494
    Beverages                57    73       53        47
    Soft_drinks            1374  1256     1572      1506
    Alcoholic_drinks        375   475      458       135
    Confectionery            54    64       62        41

``` r
dim(x)
```

    [1] 17  4

> Q2. the `row.names = 1` way because it was a little more simple to use

> Q3.

``` r
barplot(as.matrix(x), beside=T, col=rainbow(nrow(x)))
```

![](lab7bimm143_files/figure-commonmark/unnamed-chunk-18-1.png)

to make the plot the other bar style you change `beside=T` to `beside=F`

``` r
barplot(as.matrix(x), beside=F, col=rainbow(nrow(x)))
```

![](lab7bimm143_files/figure-commonmark/unnamed-chunk-19-1.png)

> Q4(5). it means these are the axis for each plot

``` r
pairs(x, col=rainbow(nrow(x)), pch=16)
```

![](lab7bimm143_files/figure-commonmark/unnamed-chunk-20-1.png)

so the paris plot is usful for small datasets but it can be lots of work
to interpret and gets interactable for longer datasets

So PCA to the rescue… the main function to do PCA in base Ris called
`prcomp()`. this function wants the transpof our datain this case.

``` r
t(x)
```

              Cheese Carcass_meat  Other_meat  Fish Fats_and_oils  Sugars
    England      105           245         685  147            193    156
    Wales        103           227         803  160            235    175
    Scotland     103           242         750  122            184    147
    N.Ireland     66           267         586   93            209    139
              Fresh_potatoes  Fresh_Veg  Other_Veg  Processed_potatoes 
    England               720        253        488                 198
    Wales                 874        265        570                 203
    Scotland              566        171        418                 220
    N.Ireland            1033        143        355                 187
              Processed_Veg  Fresh_fruit  Cereals  Beverages Soft_drinks 
    England              360         1102     1472        57         1374
    Wales                365         1137     1582        73         1256
    Scotland             337          957     1462        53         1572
    N.Ireland            334          674     1494        47         1506
              Alcoholic_drinks  Confectionery 
    England                 375             54
    Wales                   475             64
    Scotland                458             62
    N.Ireland               135             41

``` r
pca <- prcomp(t(x))
summary(pca)
```

    Importance of components:
                                PC1      PC2      PC3       PC4
    Standard deviation     324.1502 212.7478 73.87622 3.176e-14
    Proportion of Variance   0.6744   0.2905  0.03503 0.000e+00
    Cumulative Proportion    0.6744   0.9650  1.00000 1.000e+00

``` r
attributes(pca)
```

    $names
    [1] "sdev"     "rotation" "center"   "scale"    "x"       

    $class
    [1] "prcomp"

``` r
pca$x
```

                     PC1         PC2        PC3           PC4
    England   -144.99315   -2.532999 105.768945 -4.894696e-14
    Wales     -240.52915 -224.646925 -56.475555  5.700024e-13
    Scotland   -91.86934  286.081786 -44.415495 -7.460785e-13
    N.Ireland  477.39164  -58.901862  -4.877895  2.321303e-13

A MAJOR pcA result viz is called a “PCA plot” (aka a score plot, biplot,
pc1 vs pc2 plot, ordination plot)

``` r
mycols <- c("orange", "red", "blue", "darkgreen")
plot(pca$x[,1], pca$x[,2], col=mycols, pch=16, xlab="PC1", ylab="PC2")
abline(h=0, col="gray")
abline(v=0, col="gray")
```

![](lab7bimm143_files/figure-commonmark/unnamed-chunk-24-1.png)

another important output from PCA is called the “loadings” vector or the
“rotation” component - this tells us how much the original variabls (the
foods in this case)

``` r
pca$rotation
```

                                 PC1          PC2         PC3          PC4
    Cheese              -0.056955380  0.016012850  0.02394295 -0.694538519
    Carcass_meat         0.047927628  0.013915823  0.06367111  0.489884628
    Other_meat          -0.258916658 -0.015331138 -0.55384854  0.279023718
    Fish                -0.084414983 -0.050754947  0.03906481 -0.008483145
    Fats_and_oils       -0.005193623 -0.095388656 -0.12522257  0.076097502
    Sugars              -0.037620983 -0.043021699 -0.03605745  0.034101334
    Fresh_potatoes       0.401402060 -0.715017078 -0.20668248 -0.090972715
    Fresh_Veg           -0.151849942 -0.144900268  0.21382237 -0.039901917
    Other_Veg           -0.243593729 -0.225450923 -0.05332841  0.016719075
    Processed_potatoes  -0.026886233  0.042850761 -0.07364902  0.030125166
    Processed_Veg       -0.036488269 -0.045451802  0.05289191 -0.013969507
    Fresh_fruit         -0.632640898 -0.177740743  0.40012865  0.184072217
    Cereals             -0.047702858 -0.212599678 -0.35884921  0.191926714
    Beverages           -0.026187756 -0.030560542 -0.04135860  0.004831876
    Soft_drinks          0.232244140  0.555124311 -0.16942648  0.103508492
    Alcoholic_drinks    -0.463968168  0.113536523 -0.49858320 -0.316290619
    Confectionery       -0.029650201  0.005949921 -0.05232164  0.001847469

PCA looks to be a super useful method for gaining some insight into high
dimensional data that is difficult to examine in other ways
