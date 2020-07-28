# IonBreeders_IMPUTATION version 1.01
Genotype pre-imputation filtering and imputation plugin for the Ion Torrent NGS platform.


[IonBreeders_IMPUTATIONの使い方 日本語版 ver.1.01 ](https://github.com/DEMETER298/IonBreeders_IMPUTATION/wiki)


# 1. Installation Instructions

## Download plugins
 
The IMPUTATION plugin of IonBreeders is provided as a zipped package containing files from the Latest Release project page on Github. The file name will be of the format IonBreeders_IMPUTATION.zip.
1. Click the **`IonBreeders_Imputation.zip`** in the upper right and it will be displayed below **`View raw`** 
2. Click the **`View raw`** and save the zip file to you local computer. (right click on the Windows, one click on the Mac)
3. Don't unzip the downloaded IonBreeders_Imputation.zip file.

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

### 2-1 Function　＊

(1)	Remove markers with identical genotypes. (“comparegeno”, “findDupMarkers”, “drop.markers”)

(2)	Remove nonpolymorphic sites for all samples. (“pull.geno”, “drop.markers”)

(3)	Remove markers with high proportion of missing genotypes. (“drop.markers”)

(4)	Remove samples with high proportion of missing genotypes. (“drop.markers”)

(5)	Remove high heterogeneity markers. (“pull.geno”, “drop.markers”)

(6)	Remove markers with segregation distortion. (“geno.table”, “totmar”, “drop.markers”)

(7)	Impute missing genotypes using neighboring genotypes and the genetic distance or physical distance of each marker. (“fill.geno”)

(8)	Output of genotype image: output the image of the genotype and marker positions on chromosomes before and after imputation (“geno.image”, “plotMap”). Output the image of LOD scores and recombination fractions between pairs of markers. (“plotRF”)

(9)	Integration of perfectly linked markers. 

＊The parenthesis on the right indicates the function of R/qtl used in the step.


<br>
### 2-2 Input file

(1)	Prepare the genotype data of each sample in CSV format as follows; alternatively, the CSV output file (`ABH(R/qtl,IonBreeders)`) of the ABH plugin can be used.  
* The CSV file opened in Excel is shown below.
      <img src="https://user-images.githubusercontent.com/40309394/65671484-4d5fb900-e082-11e9-9b82-8caf8e2905c5.png" width="600"> 
 
(2)	Prepare the genetic distance as a CSV file in the following format. This file can be edited and save in Excel. The genetic distance can be an estimated value.  
*  The CSV file opened in Excel is shown below.
 ![distance_file](https://user-images.githubusercontent.com/40309394/65736913-b47b7d00-e117-11e9-8019-12c086bcea37.png)

 
 
### 2-3 Execution

(1)	From the list of plugins, click IonBreeders_IMPUTATION.

(2)	Set each item on the screen a shown below.

<kbd><img src="https://user-images.githubusercontent.com/40309394/65737626-ff968f80-e119-11e9-8674-7747b8abd3e1.png" /></kbd>
 
`Exclude markers with a uniform genotype for all samples` : exclude nonpolymorphic markers (eg, all samples are "B")

`Exclude markers with a genotyping rate < X% ` : exclude high missing genotype markers.

`Exclude samples with less than X% of markers genotyped` : exclude high missing genotyped samples.

`If more than X% of samples were genotyped, remove the perfectly correlated markers retaining one representative`  : exclude linked markers. (default is 95%) (eg, variant derived from same amplicon)

`Exclude markers showing a distorted segregation rate with a p-value lower than X` : exclude distorted markers (default is 0.0000000001)

`Exclude markers with a ratio of Hetero calls greater than X%` : exclude high heterogeneity markers derived from mis-mapping (default is 90%)

`Impute the genotype` : Impute the genotype based on the selected genetic distance method among four options: imp, argmax, maxmarginal ,or no_dbl_XO (see below for detailed descriptions)

`2nd imputation` can only be selected when maxmarginal is selected as the genetic distance method. Remove suspicious genotypes by maxmarginal and impute the genotype by argmax. Note that this method is only appropriate for practical breeding purposes and is not recommended for research use.

`Output of genotype image` : Images of the genotype and physical position of markers before and after filtering and imputation is output. And an image of LOD scores and recombination fractions between pairs of markers is output. 

`Output file name prefix` : Enter the desired file name.  


<br>
**Imputation methods:**

`imp`: a single random imputation is performed using sim.geno.

`argmax`: for each individual, the most probable sequence of genotypes is determined given the observed data (via argmax.geno).

`maxmarginal`: the conditional genotype probabilities are calculated with calc.genoprob, and the most probable genotype is determined for each marker. This is taken as the imputed genotype if the probability is greater than min.prob; otherwise it is considered as a missing genotype.

`no_dbl_XO`: non-recombinant intervals are filled in; recombinant intervals are left missing.  
             (ex: A---A---H---H---A → AAAAA---HHHHH---A).  

<br>
### 2-4 Output contents

When execution is completed, the following items are displayed on the screen.
　　　<img src="https://user-images.githubusercontent.com/40309394/65763462-73f32200-e15e-11e9-9cae-6683289b0734.png">  

`input file=`: Genotype file entered in the plugin screen.

`output genotype (R/qtl,IonBreeders)`: Genotype data for R/qtl format.

`output genotype (Antmap)`: Genotype data for Antmap format.

`output genotype (MAPMAKER)`: Genotype data for MAPMAKER format.

`prep file for MAPMAKER`: prep file for MAPMAKER.

`marker names for MAPMAKER`: Correspondence table of marker names for IonBreeders/R(qtl) and MAPMAKER. Convert to marker name AMPLXXXX character limit in MAPMAKER.

`marker names for MAPMAKER`: Genotype data for MapMaker format. Owing to the limit of the number of characters in MapMaker, the marker name is converted to AMP0001~AMPL9999 to support the character limit in MAPMAKER.
　　<div align="center">
    <img src="https://user-images.githubusercontent.com/40309394/65842464-c4d56700-e366-11e9-8c23-6cddb31d8d7e.png" width="300">  
　　</div>  
`genotype image`: Image file of the genotype before and after imputation is output.

`output sample list`: List of sample names

`list of removed perfectly linked markers`: Correspondence table of removed markers and integrated perfectly linked markers. The CSV file opened in Excel is shown below.    
 　　<div align="center">
     <img src="https://user-images.githubusercontent.com/40309394/65842473-d454b000-e366-11e9-9574-2582c575e307.png"  width="400">
 　　</div>   
   
***

# Contact
Eri Ogiso-Tanaka, Ph.D. demeter298(at)gmail.com

Institute of Crop Science / National Agriculture and Food Research Organization
2-1-2, Kannondai, Tsukuba, Ibaraki 305-8518, Japan

# Version
Version 1.01   (12 Mar 2020 update)

# Citing IonBreeders
Ogiso-Tanaka E, Yabe S and Tanaka T (2020)

**IonBreeders: automated bioinformatics plugins toward genomics-assisted breeding.**

Breeding Science 70（３）: 396-401.

https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7372021/


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
