

# An Empirical Study of Method Chaining in Java


## Authors:

 Tomoki Nakamaru  
     ![Author Avatar](./image1.jpg)



 Tomomasa Matsunaga

 Tetsuro Yamazaki

 Soramichi Akiyama

  ![Author Avatar](./image2.jpg)

   Shigeru Chiba

  ![Author Avatar](./image3.jpg)

 # Track: MSR 2020 Technical Papers


## On  
Mon 29 Jun 2020 10:48 - 10:54 at MSR:Zoom - Programming Languages & Models Chair(s): Dimitris Kolovos


## Abstract

 Although chaining procedures are a major instructional technique used in training severely handicapped learners, very little is known about which of these procedures (i.e., forward and backward chaining and total task presentation) has the most beneficial effect on learning. In this paper studies that have compared these chaining procedures are reviewed along the dimensions of independent variables, dependent variables, subject variables, apparatus variables, design, and method of analysis. In general, results of studies are mixed. Potential explanations of differences are offered. Procedures are then examined to see which of the procedures creates an optimal picture of learning and procedural variation which may effect such learning is investigated. Guidelines for future research and assistance for interpreting the present investigations are offered.. We then explore language features that
are helpful to the method-chaining style but have not been supported yet in Java. For this aim, we conducted manual inspections
of method chains that are randomly sampled from the collected
repositories. We also estimated how effective they are to encourage
the method-chaining style if they are adopted in Java.If you do everything in a single statement then that is
compact, but it is less readable (harder to follow) most
of the times than doing it in multiple statements.
Another post mentions that method chaining makes code confusing
since it hides the type of an object that a programmer operates upon.
Negative opinions are not only about code readability. One post in
the thread [8] states that method chaining is not reconcilable with
most debuggers that offer line-level breakpoints:
You can’t put the breakpoint in a concise point so you
can pause the program exactly where you want it. If
one of these methods throws an exception, and you
get a line number, you have no idea which method in
the “chain” caused the problem.

 Method Chaining is the practice of calling different methods in a single line instead of calling different methods with the same object reference separately. Under this procedure, we have to write the object reference once and then call the methods by separating them with a (dot.).

 ## IS METHOD CHAINING ACCEPTED?

As they described in Section 1, they measure the frequency of method
chaining to judge whether it is accepted in the real world. In their
analyses, they use only the code that is newer than or in 2010. 2010
is the year in which the number of repositories exceeds 250 and
in which the number of files exceeds 105
for the first time. They
adopt this criterion to avoid that the programming styles of a small
number of old repositories overly affect our analysi.




## Changes of quartiles from 2010 to 2018
___
1st quartile  =+1.71%

2nd quartile = +4.27%

3rd quartile = +7.34%

4th quartile = +7.08%

----


To better understand the trends in method chaining, we manually
categorized the method chains in 2018 and 2010 by their behaviors.
For this analysis, we divided the set of method chains into three
groups by their length: Short, Long, and ExtLong. 
the range of lengths and the number of chains for each group.chose the border length 8 and 42 in consideration of 𝑢𝑛 values,
the ratio of repositories that contain one or more method chains
whose length is longer than or equal to 𝑛. In 2018, more than 50%
of repositories contain chains longer than 8, and less than 5% of
repositories contain chains longer than 42, as shown in Figure 5.
Since it is not feasible to manually inspect all the chains in Short
and Long, we analyze randomly-sampled 280 method chains in
each of those groups. We analyze all the chains in ExtLong.
We categorized a method chain into either of Accessor, Builder,
Assertion, and Others. Figure 7 describes the first three of them
by example. Others is the category for chains that do not match
any of Accessor, Builder, and Assertion.
Figure 8 illustrates the ratios of each category in Short and
Long. The black bars in the figure indicate the margin of errors
due to the sampling at a 95% level of confidence. Since we did not
find any Accessor chain in the samples of Long, no blue bars are
drawn in Long. The error bar for Assertion in Long in 2010 is not
drawn since the number of chains is too low to compute its valid
margin. All the chains in ExtLong are categorized into Builder in
both 2010 and 2018.


----
Builder. A chain that builds an object. It often ends with the
invocation of a method named like buildFoo or toFoo.
// Mockito
when ( myHttpClient . execute ( capt . capture ()))
. thenReturn ( myHttpResponse );
verify ( map ). containsKey (" testOk ");
// AssertJ
assertThat ( kunaTimeTicker . getTicker ()). isNotNull ();
Assertions
. assertThat ( actualObj . has (" outline_colors "))
. isTrue ();

---




## Extremely Long Chains
Since we did not immediately see why and how such long chains
exist in the real-world code, we conducted further inspection of the
chains in ExtLong in 2018.
 How much of the ExtLong chains are in testing code? We
found 140 chains (50% of ExtLong) in testing code. As mentioned
above, all the chains in ExtLong are composed to build an object.
Thus, half of the ExtLong chains build objects for testing.
 Are the ExtLong chains machine-generated? We found only
five generated chains (1.79% of ExtLong). All of those chains
are generated by aws-java-sdk-code-generator. Most chains
in ExtLong are very likely to be written by human programmers.
 Which libraries produce the ExtLong chains? To answer this
question, we checked the package name of the first method invocation of each chain. We found 71 different package names, which
indicates that various libraries are used to compose extremely long
chains. However, a large bias exists in the number of appearances
of each library: 53.5% of the libraries are used only once; Three
libraries constitute 43.9% of the appearances. The following summarizes the most-used three libraries:


 + Elasticsearch4:
 They found 75 chains (26.8%) using XContentFactory
or XContentBuilder in this library. Those classes are for building
data used in Elasticsearch.
+ Guava5:
 They found 30 chains (10.7%) using immutable collection
builders (e.g. ImmutableSet.Builder) in this library.
Java Std. Lib. They found 18 chains (6.43%) using StringBuilder
or StringBuffer in java.lang

                        THE END