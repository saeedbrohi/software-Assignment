

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