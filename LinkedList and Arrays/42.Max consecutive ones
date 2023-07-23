class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
       int sum = 0, maxSum = 0;
       for(int n : nums) {
           sum += n;
           sum *= n;
           maxSum = Math.max(maxSum, sum); 
       } 
       return maxSum;
    }
}
