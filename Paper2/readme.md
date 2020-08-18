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
was incorrect
Results. In total, from 2019-10-15 to 2019-10-17, they sent out
emails to 246 developers. Of these, 32 could not be delivered. They
performed the sending out in three batches and used the first author’s academic email address as the sender. All emails were specific
to each recipient. They only sent one mail per recipient. They received
answers from 61 developers, corresponding to 144 build logs with
a response rate of 24.8%. Compared to typical response rates to
cold calling known from Software Engineering [16], this is very
high. They believe that their personalization and the ease of use for the
participant are the main reasons for this—simply clicking on a link
to confirm or refute an answer is enough, there is no need to craft
an answer. Indeed, they only received seven replies from developers
along the lines of “done.”
Of the 144 answers, 118 initially indicated that their extraction
was correct. They manually inspected the 26 negative answers and
found that some stated that the proposed extraction did not show
the whole description of why the build failed. This was because They
chose to trim long chunks to keep the mails readable, and not a fault
in their extraction per se. After adjusting for these answers, only
12 answers remained that stated that their labeled log chunk was
not correct. This validates our data set with an externally validated
consensus on 94.4% of the extracted data.
One of their 12 incorrect extractions only showed a warning and
the developer proposed to also include the line stating that warnings
are treated as errors. In others, we labeled the error message of an
error that was later ignored.

 ## DATA SCHEMA

This section presents the internal structure and data schema of
LogChunks. In principle, LogChunks comprises automatically retrieved and manually labeled and cross-validated logs.
LogChunks comprises information on 797 build logs, which are
organized in folders for each language and repository. For each
repository, LogChunks has about 10 Examples. Every repository
folder contains the full log files for the build status ‘failed’ in plain
text.
Structural Category. For each repository, they assign structural
categories to the Chunks. The structural category compares how
Chunks are represented within the build log. Build tools highlight
their error messages with markings, e.g. starting each line with
“ERROR” or surrounding special characters. Two chunks fall into
the same structural categories if they are surrounded by the same
markings. Listing 2 presents a log chunk from the same category.
 In comparison to that, Listing 3
presents a log chunk which is formatted differently within the log
file. For each repository, the structural categories are represented
as integers, starting at 0 and increased with the next appearing
category in chronological build order.


## RELATED DATA SETS
This section presents existing data sets of CI build logs and how
LogChunks differs from them.

  + TravisTorrent

TravisTorrent [3] collects a broad range of metadata about Travis CI
builds. It combines data accessible through the public Travis CI and
GitHub APIs and through GHTorrent [9]. Similar to LogChunks,
among the metadata are the failing test cases. However, TravisTorrent obtained these through a manually developed parser, which
only supports specific Ruby test runners and Java Maven or JUnit
logs. Anecdotally, many of the failing tests are at least incomplete
and lack validation. By contrast, LogChunks provides manually labeled and two-fold cross-validated data of why builds failed, not
only for failing tests like TravisTorrent, but for all possible buildfailing errors.


## FUTURE EXTENSIONS TO LOGCHUNKS
In this section, they describe current limitations and future improvements of LogChunks and extensions they are planning.
Chunk as One Consecutive Substring. The Chunk contains only
one continuous substring of the log text. The reason a build failed
could be described at multiple locations within the log. They propose
to extend LogChunks to contain multiple substrings of the log text.
Include More Repositories and Logs. LogChunks encompasses a
range of repositories from various main development languages,
though only 10 logs from each repository. Including more logs and
repositories will strengthen LogChunks as the go-to benchmark.
Classification of the Build Failure Cause. Our data set contains
no further classification according to the cause of the failure, such
as due to tests, compilation or linter errors. As researchers are
investigating why CI builds fail, a useful extension is to annotate
cause of the build failure for each log.
Other Information Chunks. Build log analysis is not limited to the
chunk that describes why a build failed. LogChunks can be extended
with labels for all information that is contained in the build log,
such as descriptions of warnings, build infrastructure and more.
Validation of Search Keywords. The keywords LogChunks provides are based on the experience of the authors gained from analyzing around 800 build logs. Next, they propose to evaluate whether
these keywords would also be used by developers to find the log
chunk describing why a build failed.

                             THE END