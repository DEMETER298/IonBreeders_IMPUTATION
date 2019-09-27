# IonBreeders_IMPUTATION version 1.0
Genotyping plugins for the Ion Torrent NGS platform.


[IonBreeders_IMPUTATIONの使い方 日本語版 ver.1.0 ](https://github.com/DEMETER298/IonBreeders_IMPUTATION/wiki)


# 1. Installation Instructions

## Download plugins
 
The three plugins of IonBreeders are provided as a zipped package containing files from the Latest Release project page on Github. The file name will be of the format IonBreeders_Imputation.zip.

## Install

Automatic installation from the Torrent Browser Plugin

Follow these steps for automatic installation of a plugin from the Torrent Browser:
1.	In your Torrent Browser, click the gear menu (near the top right) and select Plugins

![1](https://user-images.githubusercontent.com/40309394/54818632-14aee380-4cdd-11e9-845c-7c7d8ac95a1f.png)
  
2.	In the Plugins tab, click the **`Install or Upgrade Plugin`** button: 

![2](https://user-images.githubusercontent.com/40309394/54819228-8fc4c980-4cde-11e9-92ba-1d4b64e70e64.png) 

3.	In the **`Install or Upgrade Plugin`** tab, select downloaded IonBreeders_Imputation.zip, and click **`Upload and Install`**.  
 
![3](https://user-images.githubusercontent.com/40309394/54819317-e29e8100-4cde-11e9-91a8-3873b1263a93.png)



# 2. Plugin manuals
## 2-2 IMPUTATION plugin

### 2-2-1 Function

(1)	Remove non-informative markers, including markers with high missing rates, segregation-distorted markers, and integration of perfectly linked markers.

(2)	Remove high heterogeneity markers derived from mis-mapping.

(3)	Remove nonpolymorphic sites for all samples.

(4)	Impute missing genotypes using neighboring genotypes and the genetic or physical distance of each marker.

(5)	Output the image of the graphical genotypes and marker positions on chromosomes before and after imputation.

(6) Output the image of LOD scores and recombination fractions between pairs of markers.


### 2-2-2 Input file

(1)	Prepare the genotype data of each sample in CSV format as follows; alternatively, the CSV 
output file (ABH R/qtl) of the ABH plugin can be used.
 
(2)	Prepare the genetic distance as a tab-delimited text file in the following format. 
The genetic distance can be an estimated value.
 

### 2-2-3 Execution

(1)	From the list of plugins, click IonBreeders_Imputation.

(2)	Set each item on the screen a shown below.

![image](https://user-images.githubusercontent.com/40309394/54862886-68283c80-4d84-11e9-90c5-c57cb4c92167.png)
 
* Exclude markers with a uniform genotype for all samples.

* Exclude markers with a genotyping rate < X% (Enter a value between 0 to 100 as X) 

* Exclude samples with less than X% of markers genotyped (Enter a value between 0 and 100 as X)

* If more than X% of samples were genotyped, remove the perfectly correlated markers retaining one representative (enter a value between 0 and 100 as X; the default is 70%).

* Exclude markers showing a distorted segregation rate with a p-value lower than X (enter a value between 0.0 and 1.0 as X; the default is 0.0000000001).

* Exclude markers with a ratio of Hetero calls greater than X% (enter a value between 0 and 100 as X; the default is 50%).
Impute the genotype based on the selected genetic distance method among four options: imp, argmax, maxmarginal ,or no_dbl_XO (see below for detailed descriptions). 

*  `2nd imputation` can only be selected when maxmarginal is selected as the genetic distance method. Remove suspicious genotypes by maxmarginal and impute the genotype by argmax. Note that this method is only appropriate for practical breeding purposes and is not recommended for research use.

* `Output of genotype image` : An image of the genotype before and after imputation is output.
Output file name prefix: Enter the desired file name.

**Imputation methods:**

`imp`: a single random imputation is performed using sim.geno.

`argmax`: for each individual, the most probable sequence of genotypes is determined given the observed data (via argmax.geno).

`maxmarginal`: the conditional genotype probabilities are calculated with calc.genoprob, and the most probable genotype is determined for each marker. This is taken as the imputed genotype if the probability is greater than min.prob; otherwise it is considered as a missing genotype.

`no_dbl_XO`: non-recombinant intervals are filled in; recombinant intervals are left missing.
(ex: A---A---H---H---A → AAAAA---HHHHH---A).




(3)	Output contents

When execution is completed, the following items are displayed on the screen.
 
![image](https://user-images.githubusercontent.com/40309394/54862934-395e9600-4d85-11e9-877f-e940bf2720f9.png)

`genotype data before excluding perfectly correlated markers`: Genotype file entered in the plugin screen.

`input file`: Genotype file with perfectly lined markers removed.

`output genotype (R/qtl)`: Genotype data for R/qtl format.

`output genotype (Antmap)`: Genotype data for Antmap format.

`output genotype list (MAPMAKER)`: List of marker names

`marker names for MAPMAKER`: Genotype data for MapMaker format. Owing to the limit of the number of characters in MapMaker, the marker name is converted to AMPXXXX format from AMP0001.

`genotype image`: Image file of the genotype before and after imputation is output.

`output sample list`: List of sample names


***

# Contact
Eri Ogiso-Tanaka, Ph.D. demeter@affrc.go.jp

Institute of Crop Science / National Agriculture and Food Research Organization
2-1-2, Kannondai, Tsukuba, Ibaraki 305-8518, Japan

# Version
Version 1.0

# Citing IonBreeders
Ogiso-Tanaka E, Yabe S and Tanaka T (2019) 

**IonBreeders: semi-automated bioinformatics plugins toward genomics-assisted breeding.**

# License
NARO NON-COMMERCIAL LICENSE AGREEMENT Version 1.0

This license is for 'Non-Commercial' use of software for IonBreeders.

1. Scientific use of IonBreeders is permitted free of charge.
2. Modification of IonBreeders is only permitted to the person of downloaded and his colleagues.
3. The National Agriculture and Food Research Organization (hereinafter referred to as NARO) does not guarantee that defects, errors or malfunction will not occur with respect to IonBreeders.
4. NARO shall not be responsible or liable for any damage or loss caused or be alleged to be caused, directly or indirectly, by the download and use of IonBreeders.
5. NARO shall not be obligated to correct or repair the program regardless of the extent, even if there are any defects of malfunctions in IonBreeders.
6. The copyright and all other rights of IonBreeders belong to NARO.
7. Selling, renting, re-use of license, or use for business purposes etc. of IonBreeders shall not be allowed. For commercial use, license of commercial use is required. Inquiries for such commercial license are directed to demeter@affrc.go.jp.
8. The IonBreeders may be changed, or the distribution maybe canceled without advance notification.
9. In case the result obtained using IonBreeders in used for publication in academic journals etc., please refer the publication of IonBreeders in the publication (in preparation).


Copyright (C) 2019 [National Agriculture and Food Research Organization](https://www.naro.affrc.go.jp/english/index.html). All rights reserved.
