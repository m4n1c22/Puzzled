##Solution

###Part A

- It is probabilitic design which has 0.5 as probability for one toss. Now you need to assume to have `n` tosses and none of them needs to be dependent on each other even if you calculate the longest run of subsequence at the end.
- Now if you need to find all possible scenarios for a coin toss done say `n` times. It is real simple. Assume a number in binary format containing `n` bits. Where each bit corresponds to a head or tail. Say head being `0` and tail being `1`. Now you need to generate sequence of number for that `n` bit long number from `(0....0 to 1.....1)`. Thus convering all possible sequences.
- Now lets take an example, 3 tosses.
We could have `{HHH,HHT, HTH, HTT, THH, THT, TTH, TTT}` possible combinations.
- Now realize it in a binary format you would have `{000, 001, 010,011, 100, 101, 110, 111}`
- Such a solution is extendable to any number of `n` and also easy to implement.
- The solution complexity is dependent on the number of possible solutions which is `2^n`.
- If you need to generate random sequence it is easy pick a number from `0` to `2^n - 1` using random function generator and use the obtained number to generate the sequence.
- Consider your n = 3, random function would pick between 0 and 7.

Ideally a functional implementation of a random sequence generator in C would be:

``` C
char* generate_rand_seq(int n) {
  
  char *seq = (char*) malloc(n+1); //to avoid memory leaks

  int limit = pow(2,n);

  int rand_val = rand(limit); //generates a value between 0 and 2^n

  for(int i=0;i < n;i++) {

    seq[i] = ((rand_val>>i)&1)? 'T' : 'H';
  }

  seq[i] = '\0';

  return seq;

}
```

###Part B

Solving the part B requires the processing of longest possible continuous sequence in a list. 
You could use some inspiration from some of these works.

https://www.quora.com/How-can-we-find-the-longest-continuous-subsequence-of-0s-in-binary-representation-of-an-integer-in-O-log-n-time-complexity

###Part C

For finding if a toss is fair or not, you need to assert the fact that probability of getting 6 tosses in a row for every 1000 tosses needs to be 1. If you cannot assert this factor then your toss needs to be unfair. Generate a binomial representation for the same to assert this mathematical logic.

More information to solve using binomial distribution: http://onlinestatbook.com/2/probability/binomial.html

