# Remove duplicates from sorted Array

# Analysis
|   | 0<br/> | 1<br/> | 2<br/> | 3<br/> | 4<br/> | 5<br/> | 6<br/> | 7<br/> |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
|   | 0<br/> | 1<br/> | 2<br/> | 3<br/> | 3<br/> | 4<br/> | 4<br/> | 5<br/> |  |  |  |  |  |  |  |  |  | assign value<br/> |  |  | Notes<br/> | after run<br/> | length with no duplicates<br/> |
|  0<br/> | i<br/> | j<br/> |  |  |  |  |  |  | i==0<br/> | j==1<br/> | n[0] != n[1]<br/> | n[i] != n[j]<br/> | i++;<br/> | i == 1<br/> | j==1<br/> | i == j<br/> | n[i] == n[j]<br/> | n[i] = n[j]<br/> | n[i] = n[j]<br/> | j++<br/> | assign value doesn't affect the n[i] because before assigning the value, i already equals to j.<br/> | i=1<br/> | i+1<br/> |
|  1<br/> |  | i<br/> | j<br/> |  |  |  |  |  | i==1<br/> | j==2<br/> | n[1] != n[2]<br/> | n[i] != n[j]<br/> | i++;<br/> | i == 2<br/> | j==2<br/> | i == j<br/> | n[i] == n[j]<br/> | n[i] = n[j]<br/> | n[i] = n[j]<br/> | j++<br/> | assign value doesn't affect the n[i] because before assigning the value, i already equals to j.<br/> | i=2<br/> | i+1<br/> |
|  2<br/> |  |  | i<br/> | j<br/> |  |  |  |  | i==2<br/> | j==3<br/> | n[2] != n[3]<br/> | n[i] != n[j]<br/> | i++;<br/> | i == 3<br/> | j==3<br/> | i == j<br/> | n[i] == n[j]<br/> | n[i] = n[j]<br/> | n[i] = n[j]<br/> | j++<br/> | assign value doesn't affect the n[i] because before assigning the value, i already equals to j.<br/> | i=3<br/> | i+1<br/> |
|  3<br/> |  |  |  | i<br/> | j<br/> |  |  |  | i==3<br/> | j==4<br/> | n[3] == n[4]<br/> | n[i] == n[j]<br/> | i,  don't move<br/> | i==3<br/> | j==4<br/> | i != j<br/> | n[i] == n[j]<br/> | n[i] = n[j]<br/> | n[i] = n[j]<br/> | j++<br/> | assign value doesn't affect the n[i] because before n[i] already equals to n[j], it is the two consecuive 3<br/> | i=3<br/> | i+1<br/> |
|  4<br/> |  |  |  | i<br/> |  | j<br/> |  |  | i==3<br/> | j==5<br/> | n[3] != n[5]<br/> | n[i] != n[j]<br/> | i++;<br/> | i==4<br/> | j==5<br/> | i != j<br/> | n[i] != n[j]<br/> | n[i] = n[j]<br/> | n[i] = n[j]<br/> | j++<br/> | we copy number 4 to cover the second number 3 - acieve removing duplicates<br/> | i=4<br/> | i+1<br/> |
|   | 0<br/> | 1<br/> | 2<br/> | 3<br/> | 4<br/> | 4<br/> | 4<br/> | 5<br/> |  |  |  |  |  |  |  |  |  |  |  |  |  |  | i+1<br/> |
|  5<br/> |  |  |  |  | i<br/> |  | j<br/> |  | i==4<br/> | j==6<br/> | n[4] == n[6]<br/> | n[i] == n[j]<br/> | i,  don't move<br/> | i==4<br/> | j==6<br/> | i != j<br/> | n[i] == n[j]<br/> | n[i] == n[j]<br/> | n[i] == n[j]<br/> | j++<br/> | assign value doesn't affect the n[i] because before n[i] already equals to n[j], it is the  consecuive 4<br/> | i=4<br/> | i+1<br/> |
|  6<br/> |  |  |  |  | i<br/> |  |  | j<br/> | i==4<br/> | j==7<br/> | n[4] != n[7]<br/> | n[i] != n[j]<br/> | i++;<br/> | i==5<br/> | j==7<br/> | i != j<br/> | n[i] != n[j]<br/> | n[i] = n[j]<br/> | n[i] == n[j]<br/> | j++<br/> | we copy number 5 to cover the second number 4 - acieve removing duplicates<br/> | i=5<br/> | i+1<br/> |

Code:
     public int removeDuplicates(int[] nums) {
        int i = 0;
        for(int j = i + 1; j < nums.length; j++) {
            if(nums[j] != nums[i]) {
                i++;
            }
            nums[i] = nums[j];
        }
        return i+1;
    }

