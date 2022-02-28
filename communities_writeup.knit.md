---
title: "Community Dectection Assignment"
author: "David Terner"
date: "02/27/2022"
output: pdf_document
---















I decided to use R and Rmarkdown to complete this assignment because I wanted to experiment with systematically changing the resolution parameter (for the Louvain community detection method). By contrast,  Gephi makes it difficult to complete the same experiment. 

### Which resolution to use? 

According to the ```football.txt``` file, college team/node values correspond to team conferences. 


\begin{tabular}{l|l}
\hline
value & conference\\
\hline
0 & Atlantic Coast\\
\hline
1 & Big East\\
\hline
2 & Big Ten\\
\hline
3 & Big Twelve\\
\hline
4 & Conference USA\\
\hline
5 & Independents\\
\hline
6 & Mid-American\\
\hline
7 & Mountain West\\
\hline
8 & Pacific Ten\\
\hline
9 & Southeastern\\
\hline
10 & Sun Belt\\
\hline
11 & Western Athletic\\
\hline
\end{tabular}

I pick a resolution value $t^*$ such that: (i) the number of communities equals the number of conferences, namely 12; and, (ii) each conference has, on average, the majority of its teams belong to to the same community. I operationalize this second requirement by first computing the share of top community (largest number of occurrences) per conference group, second determining the median share, and finally adjusting the resolution parameter such that this median share is maximized. Denote this median share value as the *sameness rate*. 

I search over a grid of 100 values of the resolution parameter from 0.01 to 1.01 by 0.01 increments. 

The figure below presents the *sameness rate*- measured by the blue line and left vertical axis- and the number of communities-measured by the black line and right vertical axis-in the same plot. The red dashed lines correspond to the smallest/largest resolution values that yield 12 communities. Based on the small blue spike that is intersected by the red dashed boundary line, I choose $t^*=0.32$ as the resolution value. 

![](communities_writeup_files/figure-latex/unnamed-chunk-6-1.pdf)<!-- --> 


![](communities_writeup_files/figure-latex/unnamed-chunk-8-1.pdf)<!-- --> 
\begin{tabular}{l|r}
\hline
Conference & Top Community Share\\
\hline
Atlantic Coast & 1.00\\
\hline
Big Ten & 1.00\\
\hline
Big Twelve & 1.00\\
\hline
Mid-American & 1.00\\
\hline
Mountain West & 1.00\\
\hline
Pacific Ten & 1.00\\
\hline
Southeastern & 1.00\\
\hline
Conference USA & 0.90\\
\hline
Big East & 0.88\\
\hline
Western Athletic & 0.80\\
\hline
Sun Belt & 0.43\\
\hline
Independents & 0.40\\
\hline
\end{tabular}
Using the Forced Atlas layout, the college football league does appear to have some community structure to it. Using the $t^*=0.32$ resolution does a pretty good job matching communities to conferences: 7 out of 12 conferences consist of exactly one community. On the lower end, there is less of tight fit especially with the "Independents" conference. This shouldn't come as a shock given which schools belong to the "Independents" conference;  Central Florida, Connecticut, Navy, Notre Dame, and Utah State are clearly a diverse group of programs with little in common save football conference membership. By contrast, the "Big 10" conference is exclusive to the MidWest. 



## How are betweenness centrality and community structure related?

![](communities_writeup_files/figure-latex/unnamed-chunk-10-1.pdf)<!-- --> 
Based on the above figure, there doesn't appear to be a strong relationship between between "betweeness" and "modularity". Nodes within a community can all have betweeness scores that relatively close to one another; see communities 4+5. However for other communities, such as 6 or 12, there's substantial betweeness variation. 



