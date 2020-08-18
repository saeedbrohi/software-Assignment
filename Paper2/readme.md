# LogChunks: A Data Set for Build Log Analysis

## Authors:

Carolin Brandt

![Author Avatar](./image1.jpg)


 Annibale Panichella

 ![Author Avatar](./image2.jpg)
 
  Andy Zaidman
  
  ![Author Avatar](./image3.jpg)

   Moritz Beller

   ![Author Avatar](./image4.jpg)

   ### Track: MSR 2020 Data Showcase


   ### On:  Mon 29 Jun 2020 11:48 - 12:00 at MSR:Zoom - Build, CI, & Dependencies Chair(s): Raula Gaikovina Kula

  ## Abstract:

  They collected 797 Travis CI logs from a wide range of 80 GitHub repositories from 29 different main development languages.
we can find their collection tool in `log-collection` and the logs sorted by language and repository in `logs`.

they manually labeled the part (chunk) of the log describing why the build failed.In addition, the chunks are annotated with keywords that they would use to search for us and categorized according to our structural representation within the log.
We can find this data in an xml-file for each repository in `build-failure-reason`.
