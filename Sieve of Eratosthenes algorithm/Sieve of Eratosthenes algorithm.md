

```java
import java.util.Arrays;

public class SieveOfEratosthenes {

    public static void main(String[] args) {
        int n = 30; // Example limit
        boolean[] primes = sieveOfEratosthenes(n);
        
        // Print all prime numbers
        for (int i = 2; i <= n; i++) {
            if (primes[i]) {
                System.out.print(i + " ");
            }
        }
    }

    public static boolean[] sieveOfEratosthenes(int n) {
        boolean[] isPrime = new boolean[n + 1];
        Arrays.fill(isPrime, true);
        isPrime[0] = false; // 0 is not a prime number
        isPrime[1] = false; // 1 is not a prime number

        for (int p = 2; p * p <= n; p++) {
            // If isPrime[p] is still true, then it is a prime
            if (isPrime[p]) {
                // Mark all multiples of p as false indicating they are not primes
                for (int i = p * p; i <= n; i += p) {
                    isPrime[i] = false;
                }
            }
        }
        
        return isPrime;
    }
}
```

### Step-by-Step Explanation with Example (n = 30)

#### Initialization

```java
boolean[] isPrime = new boolean[n + 1];
Arrays.fill(isPrime, true);
isPrime[0] = false;
isPrime[1] = false;
```
- `boolean[] isPrime = new boolean[n + 1];` creates a boolean array `isPrime` of size 31, initialized to `false`.
- `Arrays.fill(isPrime, true);` sets all elements of `isPrime` to `true`.
- `isPrime[0] = false;` and `isPrime[1] = false;` explicitly mark 0 and 1 as `false` because 0 and 1 are not primes.

**State of `isPrime` array:**

```
Index:  0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30
Value:  F  F  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T
```

#### Outer Loop: Iteration for p = 2

```java
for (int p = 2; p * p <= n; p++) {
    if (isPrime[p]) {
        for (int i = p * p; i <= n; i += p) {
            isPrime[i] = false;
        }
    }
}
```

1. **Iteration with p = 2:**
   - `p * p = 4` which is less than or equal to 30.
   - `isPrime[2]` is `true`.

```java
for (int i = p * p; i <= n; i += p) {
    isPrime[i] = false;
}
```
- Inner loop starts at `i = 4` (2 * 2):
  - Mark `isPrime[4]` as `false`
  - Mark `isPrime[6]` as `false`
  - Mark `isPrime[8]` as `false`
  - Continue marking multiples of 2 (10, 12, 14, ..., 30) as `false`.

**State of `isPrime` array after marking multiples of 2:**

```
Index:  0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30
Value:  F  F  T  T  F  T  F  T  F  T  F  T  F  T  F  T  F  T  F  T  F  T  F  T  F  T  F  T  F  T  F
```

#### Outer Loop: Iteration for p = 3

2. **Iteration with p = 3:**
   - `p * p = 9` which is less than or equal to 30.
   - `isPrime[3]` is `true`.

```java
for (int i = p * p; i <= n; i += p) {
    isPrime[i] = false;
}
```
- Inner loop starts at `i = 9` (3 * 3):
  - Mark `isPrime[9]` as `false`
  - Mark `isPrime[12]` as `false`
  - Mark `isPrime[15]` as `false`
  - Continue marking multiples of 3 (18, 21, 24, 27, 30) as `false`.

**State of `isPrime` array after marking multiples of 3:**

```
Index:  0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30
Value:  F  F  T  T  F  T  F  T  F  F  F  T  F  T  F  F  F  T  F  T  F  F  F  T  F  T  F  F  F  T  F
```

#### Outer Loop: Iteration for p = 4

3. **Iteration with p = 4:**
   - `p * p = 16` which is less than or equal to 30.
   - `isPrime[4]` is `false` (it was marked by 2's iteration).

- Skip to the next `p`.

#### Outer Loop: Iteration for p = 5

4. **Iteration with p = 5:**
   - `p * p = 25` which is less than or equal to 30.
   - `isPrime[5]` is `true`.

```java
for (int i = p * p; i <= n; i += p) {
    isPrime[i] = false;
}
```
- Inner loop starts at `i = 25` (5 * 5):
  - Mark `isPrime[25]` as `false`
  - Mark `isPrime[30]` as `false`

**State of `isPrime` array after marking multiples of 5:**

```
Index:  0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30
Value:  F  F  T  T  F  T  F  T  F  F  F  T  F  T  F  F  F  T  F  T  F  F  F  T  F  F  F  F  F  T  F
```

#### Outer Loop: Iteration for p = 6

5. **Iteration with p = 6:**
   - `p * p = 36` which is greater than 30.
   - The outer loop condition `p * p <= n` fails, so the loop exits.

### Printing Prime Numbers

```java
for (int i = 2; i <= n; i++) {
    if (isPrime[i]) {
        System.out.print(i + " ");
    }
}
```
- This loop goes through the `isPrime` array from 2 to 30 and prints the indices that are marked as `true`.

**Output:**

```
2 3 5 7 11 13 17 19 23 29
```

These are the prime numbers up to 30.

### Summary

- **Initialization:** We set up the boolean array to assume all numbers are prime except for 0 and 1.
- **Outer Loop:** We iterate through each number starting from 2 up to the square root of `n`.
- **Inner Loop:** For each prime number `p`, we mark its multiples as non-prime.
- **Printing Primes:** Finally, we print all numbers that remain marked as prime.

