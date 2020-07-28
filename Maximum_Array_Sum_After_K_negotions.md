
# [maximize-sum-of-array-after-k-negations](https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/)
## Thoughts:
   1. Case based problem. 
       
## methods: 
	   1. Need sorting
	   2. As  100 <= A[i] <= 100 got counting sort. 
      
## greedy approach:
	   1. find the frequency of each number.
	   2. iterate from negative number to positive number:
	      a) for negative number if chance for negotiation do that. 
	   3. corner case : when there is no negative number in 
	      that case change the sign of smallest non-negative number.
         
## Pseudo-code:
		public int largestSumAfterKNegations(int[] A, int K) {
		  int[] cnt = new int[201];
		  int res = 0;
		  for (int i : A) ++cnt[i + 100];
		  for (int i = -100; i <= 100 && K > 0; ++i) {
		    if (cnt[i + 100] > 0) {
		      int k = i < 0 ? Math.min(K, cnt[i + 100]) : K % 2;
		      cnt[-i + 100] += k;
		      cnt[i + 100] -= k;
		      K = i < 0 ? K - k : 0;
		    }
		  }
		  for (int i = -100; i <= 100; ++i) res += i * cnt[i + 100];
		  return res;
		}
## time-complexity: O(n)
## space complexity: O(1)

            

