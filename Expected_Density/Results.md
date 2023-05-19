I wanted to do some checks on the behavior of my program and so I decided to throw together some software to look at the desnity of minimizers, $\frac{number-of-minimizers}{number-of-total-kmers}$.
# Set Up
For this series of experiments, the small window size was set to 16 for everything, and the sequence length was set to $10^5$. I wrote a program to randomly generate 100 sequences that only contained ACTG characters and another 100 sequences that could contain the character N, along with ACTG characters. So for the ACTG only sequences, there are 99985 kmers, and for the non-ACTG allowed sequences, the probability of a character being N was set to 1/17, and on average the number of kmers was between 61000 and 62000. The program I wrote does an actual count of how many k-mers are in the sequence following the same skipping rules that the Digester does. 
For the Mod Minimizer, I ran tests using 4 different mod values, M, 2 prime and 2 not prime. I thought of X as a Bernoulli(1/M) representing the probability that a given kmer in the sequence was a minimizer. 
For the [Window Minimizer](https://academic.oup.com/bioinformatics/article/33/14/i110/3953951) and [Syncmer](https://peerj.com/articles/10805/), apparently the expected density of minimizers is $\frac{2}{w+1}$, where w is the number of kmers in the large window. Although the way I implemented Syncmers is a bit different from what is described in the paper because I don't break ties for Syncmers, I just check to make sure that the smallest hash value in the large window is also equal to either the hash value of the leftmost or rightmost kmer. But, since w is set to 16, and ntHash is a 64 bit hash, the probability of ties is basically zero.
# Results
The graphs for the set of tests run on the ACTG only sequences are in the ACTG_Only_Graphs folder and the graphs for the set of tests run on sequences that contained N are in the Not_ACTG_Only_Graphs folder. 