# LintCode 143 · Sort Colors II

# LintCode **# 143 · Sort Colors II**# 

public class Solution {
    /**
     * @param colors: A list of integer
     * @param k: An integer
     * @return: nothing
     */
    public void sortColors2(int[] colors, int k) {
        // write your code here
        rainbowSort(colors, 0, colors.length - 1, 0, k );
    }

    private void rainbowSort(int[] colors, 
                            int left,
                            int right,
                            int colorL, 
                            int colorR) {
        if (colorL == colorR) return;
        if (left >= right) return;

        int colorMid = (colorL + colorR) / 2;
        int l = left;
        int r = right;
        while (l < r) {
            while (l < r && colors[l] <= colorMid) {
                l++;
            }
            while (l < r && colors[r] > colorMid) {
                r--;
            }

            if (l < r) {
                int temp = colors[l];
                colors[l] = colors[r];
                colors[r] = temp;

                l++;
                r--;
            }
        }

        rainbowSort(colors, left, l, colorL, colorMid);
        rainbowSort(colors, r, right, colorMid + 1, colorR);

    }
}

![LintCode 143 · Sort Colors II](images/LintCode%20143%20·%20Sort%20Colors%20II.png)

![LintCode 143 · Sort Colors II-1](images/LintCode%20143%20·%20Sort%20Colors%20II-1.png)

