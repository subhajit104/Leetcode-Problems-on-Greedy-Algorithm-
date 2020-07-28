# link: https://leetcode.com/problems/two-city-scheduling/
## Thoughts:
       Need to find minimum, find optimal solution. 
## methods: 
       1. Dynamic Programing. 
       2. Greedy Algorithm 
       3. Binary Search 
# Dynamic Programming:
  ## finding states for recursion:
  1.  Need to select n candidates from city A effectively so that 
     Overall traveling cost should be minimized.
  2. Mathematical recursion : 
     F(i,n) = min(COSTA(i) + F(i-1,n-1), COSTB(i) + F(i-1,n) 

# Pseudo-code:
  
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

