# Factorization

## generating divisors of a number n:
```
List<Long> generateDivisors(Long n) {
    List<Long> divisors = new ArrayList<Long>();
    
    long i;
    for (i = 1; i*i < n; i++) {
        if (n % i == 0) {
            divisors.add(i);
            divisors.add(n/i);
        }
    }
    
    if (i*i == n) {
        divisors.add(i);
    }
}
```

## generating the prime factors of a number n:

* approach #1:
```
1. use sieve to get the prime numbers in range [2, n]
2. for each prime p:
    while (n%p == 0): 
        divisors.add(p);
        n/=p;
```
* approach #2 (more efficient):
```
List<Long> primeFactorization(Long n) {
    List<Long> primes = new ArrayList<Long>();
    
    for (long i = 2; i*i <= n; i++) {
        while (n % i == 0){
            primes.add(i);
            n /= i;
        }
    }
    
    // if n is prime it will never gets divided by any number in the above loop
    if (n > 1) {
        primes.add(n);
    }
}

```

## counting the number of divisors
    
* the second approach is much faster the first approach and is also much faster the algorithm of finding the divisors in the above point
* if you want to only count the number of divisors (you don't want to list them):
    * every number could be represented in the form -> `a^A * b^B * c^C ...`
    * now we can modify the above algorithm to return only the `[A, B, C, ...]`
    * after that the number of **divisors** equals (A+1) * (B+1) * (C+1) ...
* What about the divisors count of n^z:
    * if:   n   = p1^a  + p2^b  + p3^c
    * then: n^z = p1^az + p2^bz + p3^cz

    * divisors of n   = (a+1)  * (b+1)  * (c+1)
    * divisors of n^z = (az+1) * (bz+1) * (cz+1)

* counting the number of divisors for a range of numbers from 1 to n (or multible random numbers)
```
List<Integer> factorsFrequencyArray(int n) {
    List<Integer> divisors = new ArrayList<Integer>();
    for (int i=0; i<=n; i++) {
        for(int k=i; k<=n; k+=i) {
            factors[k]++;
        }
    }
}

public static void main(String[] args) {
    List<Integer> fq = factorsFrequencyArray(n);
    
    // for range query
    int sum = 0;
    for (int i=0; i<=n; i++) {
        sum += fq[i];
    }
    
    // for some random numbers
    int[] randomNums = new int[]{1,2,34,3,2,5};
    
    int sum = 0;
    for (var i : randomNums) {
        sum+= fq[i];
    }

}

```
