# CMPS 2200 Assignment 3
## Answers

**Name:** Lulu Sawaf


Place all written answers from `assignment-03.md` here for easier grading.

1a)
Find the highest value power of 2, x, for 2^x, where x <= N. Update N, N -= x, repeat with next value x so x <= N (the new N-x). repeat until N = 0
demonstrated in min_coins function.

1b)
min_coins always chooses largest possible coin, aka value x, at every iteration. Since x is a power of 2, less optimal values will only sum to N with more coins, so the values that sum to N with fewer coins will be chosen

1c)

Work = Span = O(logn)

2a) imagine D = {1, 3, 4} and N=6

Greedy algorith picks the first coin power of 2 <= 6, which is 4 remainder 2. Then it will pick the largest coin power of 2 <= 2, which is 1 (picked 2 times)
This ywilds 4 + 1 + 1, or 3 coins
Optimally it should be 3 + 3, or 2 coins

2b

Let OPT(n) be the minimum number of coins required to make change for amount n using coin denominations D = [d₀, d₁, ..., dₖ₋₁]. Then:

OPT(n) = min_{i | dᵢ ≤ n} (OPT(n − dᵢ) + 1)

That is, the optimal number of coins for amount n is the minimum of 1 plus the optimal solution to the subproblem of making change for n − dᵢ, for all coin denominations dᵢ ≤ n.

Proof:
Let S be an optimal solution for amt n. Suppose first coin used in S is of denomination dⱼ. The rest of the coins in S must form an optimal solution for amount n − dⱼ becayse if there were a better way to make change for n − dⱼ, we could replace the sub-solution and get a better overall solution for n, contradicting the assumption that S was optimal.

This proves that the problem exhibits optimal substructure, since the solution to the whole problem involves solving smaller subproblems optimally.

2c

  def min_coins(D, N):
  
    dp = [float('inf')] * (N + 1)
    dp[0] = 0  # Base case
    for amount in range(1, N + 1):
        for coin in D:
            if coin <= amount:
                dp[amount] = min(dp[amount], dp[amount - coin] + 1)

    return dp[N] if dp[N] != float('inf') else -1  # Return -1 if change is impossible
    
work: O(N*K) span: O(N)
