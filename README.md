# Distinct-Subsequences

Given two strings s and t, return the number of distinct subsequences of s which equals t.
The test cases are generated so that the answer fits on a 32-bit signed integer.

class Solution:
    def numDistinct(self, s: str, t: str) -> int:
        ls = len(s)
        lt = len(t)
        dp = [[-1 for i in range(lt)] for j in range(ls)]
        return self.count1(s,t,ls-1,lt-1,dp)
    
    
    def count1(self,s1, s2, ind1, ind2, dp):
        if ind2 < 0:
            return 1
        if ind1 < 0:
            return 0
    
        if dp[ind1][ind2] != -1:
            return dp[ind1][ind2]

        if s1[ind1] == s2[ind2]:
            leaveOne = self.count1(s1, s2, ind1 - 1, ind2 - 1, dp)
            stay = self.count1(s1, s2, ind1 - 1, ind2, dp)
        
            dp[ind1][ind2] = (leaveOne + stay)
            return dp[ind1][ind2]
        else:
            dp[ind1][ind2] = self.count1(s1, s2, ind1 - 1, ind2, dp)
            return dp[ind1][ind2]
