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


## CREATING LOGCHUNKS:
This section presents how we gathered the logs and our manual
labeling process.

+ Log Collection
Repository Sampling. They target mature GitHub repositories that
are using Travis CI. To avoid personal and toy projects they select popular projects based on the number of users that starred.

+ Build Sampling. To sample builds for LogChunks thye keep the
ten most recent builds of the status failed [6]. They check up to 1,000
builds per repository to ensure predictable termination of the log
collection.

+ Log Sampling. Travis CI builds comprise a number of jobs that
actualize a build process in different environments. Hence, the
outcome from different jobs might be different. For each build in
LogChunks, they download the log of the first job that has the same
state as the overall build.
They inspected the collected build logs and discarded logs from
three repositories. One had only one failed build, two others had
empty build logs on Travis CI. In total, they collected 797 logs from
80 repositories spanning 29 languages.


## Manual Labeling

After collecting build logs, the first author manually labeled which
text chunk describes why the build failed. Following that, she assigned search keywords and structural categories to each log chunk.
Chunk That Describes Why The Build Failed. For each repository,
the labeler skimmed through the build logs and copied out the first
occurrence of a description why the build failed. She preserved
whitespaces and special characters, as these might be crucial to
detect the targeted substring. To support learning of regular expressions identifying the labeled substrings the labeler aimed to start
and end the labeled substring at consistent locations around the
fault description.
the Chunk and ten lines above and below. The labeler’s task was
to note down three strings they would search for (“grep”) to find
this failure description. The strings should appear in or around the
Chunk and are case-sensitive. We made no limitations on the search
string; particularly, spaces are allowed.
Structural Category. To label the structural categories we presented the Chunk and the surrounding context to the labeler for all
logs from a repository. We asked the labeler to assign numerical
categories according to whether the Chunk had the same structural
representation.



## Validation

They validated our collected data points in an iterative fashion. First,
they performed an initial inter-rater reliability study with the second
author of this paper. Our learnings from this initial internal study
are that 1) it is important and difficult to adequately communicate
all decisions and assumptions on how to and which data to label and
2) there can be different legitimate viewpoints on which log chunk
constitute the cardinal error and which keywords best to use. These
learning informed the design of a second, larger cross-validation
study for which they contacted over 200 developers.
In their second validation, we sent out emails to the original developers whose commits triggered the builds represented in LogChunks
and asked them whether the log chunk they labeled actually describes
why the build failed. This section describes our survey and discusses
our results.
Method. Using the Travis API, they collected the commit information for each build represented in LogChunks. We grouped all
commits triggered by one developer and sent out an email to them.
It included links to the corresponding commits, the build overview
and the log file. They asked the developers to fill out a short form
in case their extraction was not correct. In the survey, they asked the
developer to paste in the log part actually describing the failure
reason or describe in their own words why our original extraction
was incorrect.