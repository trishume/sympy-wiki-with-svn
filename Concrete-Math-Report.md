


# Introduction

My interest in the field of computer algebra started about a year ago. Before that most of my time I was spending on analysis of computer programming languages, compilers and operating systems design. During the previous summer I've read some introductory and very interesting papers about polynomial algorithms, term rewriting and simplification and, especially, concrete mathematics.

At first I wanted to start my own CAS project but at that time I wasn't well prepared for this task. Then I found out AXIOM and Aldor programming language. Although both fascinated me, they were to complex and had very poor developers support. After those two short episodes in computer algebra, I had several influential courses at my university: measure theory, topology and functional analysis, to name a few. They changed my view on mathematics in general and made me think on developing tools which would help with my studies and with some very preliminary research problems.

Then Google Summer of Code initialization phase started. In fact I wanted to take part in both previous editions, but during the first one I was developing operating system's nano kernel (and I wasn't a student at that time) and during the second edition I had too much work at school. However this year I've done everything to finally take part in SoC. At first I wasn't convinced what project should I work on. I was thinking on developing Scheme front end for LLVM compiler. But then I've found !SymPy, mostly by an accident.

!SymPy at that time was very small project so I thought it will a great opportunity to learn computer algebra fundamentals from very beginning. This way I convinced my self to work on this project and to propose Concrete Mathematics module, as this is a set of tools and algorithms required in every computer algebra system.

# About myself

My name is Mateusz Paprocki and I'm a student of systems engineering and computer science at the University of Technology of Wrocław in Poland. My main educational activities concern optimization, modeling and identification of complex systems and in future application of chaos theory to those fields.

# Project ideas

When I found !SymPy I didn't think long about what I can do. The first and the only idea was Concrete Mathematics, to be specific, difference equations solving and representing definite and indefinite summations in closed or pretty form. I've chosen this because I had already some preparation in this field. Also, usually people are more interested in implementing algorithms for continuous problems, so I wanted, in opposition to this tendency, implement algorithms for discrete problems. And finally, tools I've proposed are just useful for any computer science student, especially in the field of complexity analysis.

= Coding = 

In my proposal I gave detailed schedule of things I will work on. However from the very beginning I found it a bit useless as !SymPy was lacking some fundamental algorithms at that time, which were crucial parts of tools I've proposed. Also when I got deeper into the details of concepts of Concrete Mathematics and its algorithms, I saw that there were several unfortunate decisions in my proposal. First of all, at the beginning of SoC I should have worked on summations. However implementing summation algorithms is useless without proper setup of recurrence solving and simplification.

So at first I've coded several term rewriting and simplification algorithms and then I've started working on the solvers. Here I've done more than I previously expected. Mainly I intended to implement Hyper algorithm but I found that without fast algorithms for obtaining polynomial and rational solutions, it will perform poorly. This way I came to very sophisticated ABP algorithm, which can find polynomial solutions of recurrence with polynomial coefficients. Although the algorithm is complicated and it took me quite a long time to fully understand it and make it efficient at runtime, its results are sometimes amazing and can perform magnitudes faster than the classical approach.

However no matter how sophisticated algorithms I would use and how optimized my implementations were, without proper support form underlying algorithms, especially core ones, they would be useless. That's why I was for fast movement to the new core and so I spent quite much time on making it working. As a result of this now we can solve recurrences in reasonable time.

However when I was finished with all this no time left for summation algorithms implementation, mainly for Gosper's and Zeilberger's algorithms. In the mean time I found papers in which the original approaches are optimized and generalized, especially m-fold versions of those algorithms are very interesting to be implemented. Although I wasn't able to do this during SoC, I will continue my work in this field and in September I will add both to !SymPy.

# Future plans

Recurrence solving algorithms I've implemented can be adapted the case of q-difference and differential equations. So in near future I will work on this generalization, and also will finish summations as previously stated. This way I will be able to implement q-analogs of Gosper's and Zeilberger's algorithms.

# Conclusions

I'm very happy that I took part in Google Summer of Code this year and especially that I've done the coding for !SymPy. I've learned many new things during this summer about team work, project management and mathematics it self. I've found also that Python can be used for more complicated tasks, like computer algebra systems. Prior I would rather use C or O'Caml but now I see Python a better choice. 