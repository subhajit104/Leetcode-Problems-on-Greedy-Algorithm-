# [two-city-scheduling](https://leetcode.com/problems/two-city-scheduling/)
## Thoughts:
       Need to find minimum, find optimal solution. 
## methods: 
       1. Dynamic Programing. 
       2. Greedy Algorithm 
       3. Binary Search 
## Dynamic Programming:
         1. Need to select n candidates from city A effectively so that 
            Overall traveling cost should be minimized.
         2. Mathematical recursion : 
            F(i,n) = min(COSTA(i) + F(i-1,n-1), COSTB(i) + F(i-1,n) 
## Pseudo-code:
           int twoCitySchedCost(vector<vector<int>>& costs) {


               int size = costs.size();
               int n = size/2; 

               // build dp table. 
               vector< vector<int> > dp(size+1,vector<int>(n+1,inf));


               // computation F(i,0) 
               dp[0][0] = 0 ;
               for(int sum = 0, i = 0 ; i < size ; i ++)
               {
                   sum += costs[i][1];
                   dp[i+1][0] = sum ; 
               }

               // transition of states. 
               for(int i = 1 ; i <= costs.size() ; i ++)
               {
                   for(int j = 1 ; j <= min((int)costs.size()/2,i) ; j ++)
                   {
                       dp[i][j] = min(costs[i-1][0] + dp[i-1][j-1], costs[i-1][1] + dp[i-1][j]);
                   }
               }

               return dp[size][n]; 

           }

## greedy approach:  
    1. Candidates should visit city A if fare is less compare to B.  
    2. But also need to take care of higher difference  fare cost. 
    3. ow much money can we save if we fly a person to A vs. B? To
        minimize the total cost, we should fly the 
        person with the maximum saving to A,   and with the minimum - to B

## pseudo-code: 
      int twoCitySchedCost(vector<vector<int>>& cs, int res = 0) {
      sort(begin(cs), end(cs), [](vector<int> &v_1, vector<int> &v_2) {
        return (v_1[0] - v_1[1] < v_2[0] - v_2[1]);
      });
      for (auto i = 0; i < cs.size() / 2; ++i) {
        res += cs[i][0] + cs[i + cs.size() / 2][1];
      }
      return res;
      }
## Time-comlexity: O(nlogn) 
## Space-Complexity: O(1) 

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

            

