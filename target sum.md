
    public:
    int findTargetSumWays(vector<int>& nums, int target) {  
        int sum=0;
        
        for(int i=0;i<nums.size();i++){
            sum+=nums[i];
        }
        if(target>sum) return 0;
        else if(target<-sum) return 0;
        vector<vector<int>>dp(nums.size(),vector<int>(2*sum+1,0));
        
        dp[0][nums[0]+sum]+=1;
        dp[0][sum-nums[0]]+=1;
        
        for(int i=0;i<dp.size()-1;i++){
            for(int j=0;j<dp[0].size();j++){
                if(dp[i][j]==0){
                    continue;
                }
                else{
                   // cout<<i<<" "<<j<<" ";
                    dp[i+1][j-nums[i+1]]+=dp[i][j];
                    dp[i+1][j+nums[i+1]]+=dp[i][j];
                }
            }
        }
        
        return dp[dp.size()-1][sum+target];
        
    }
