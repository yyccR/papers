# Papers

[TOC]

## Preface

This project contains all kind of papers that helps me a lot at work, for example, some help me to speed up the computation of TSP problem, some help me to overcome the GPS trajectory correction, GPS trajectory section, some help me to do a better jobs in Navigation(CNNs), some help me to recommend a better route in route planning problem(RNNs) and other many many jobs, I post them here wish to help someone who needed and so that he/she can make things more better.

You can clone and share it with others, also if you have some other papers/documents/books that you think they may help others, just push them.

## Details

Below are some details about the papers in the project.

- **genetic algorithm** 

  The papers in genetic algorithm(GA) folder are mainly about TSP, and it helps me to speed up the computation and improve the accuracy of route planning. For example I implemented the GA in parallel and it was three to four times faster, left bottom is normal computation and right bottom is parallel computation in my local machine, and when I put it on the server, I run 10 threads parallel to calculate, and it can help me plan 40 points in 1-2 seconds.

  <img src="https://raw.githubusercontent.com/yyccR/Pictures/master/geneticAlgorithm/%E4%B8%B2%E8%A1%8C%E8%AE%A1%E7%AE%97GA.gif" width="398" height="200" /><img src="https://raw.githubusercontent.com/yyccR/Pictures/master/geneticAlgorithm/%E5%B9%B6%E8%A1%8C%E8%AE%A1%E7%AE%97GA.gif" width="398" height="200" />

  And the algorithm seems to work very well in TSPLIB which can be download from https://www.iwr.uni-heidelberg.de/groups/comopt/software/TSPLIB95/ . Below I show some accuracy viewer of the route planning using GA.

  <img src="https://raw.githubusercontent.com/yyccR/Pictures/master/geneticAlgorithm/44nocycle.gif" width="388" height="246" />  &nbsp; <img src="https://raw.githubusercontent.com/yyccR/Pictures/master/geneticAlgorithm/42cycle.gif" width="388" height="246" />

- ​



