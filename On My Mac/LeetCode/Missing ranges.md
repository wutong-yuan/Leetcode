# Missing ranges
public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        List<String> output = new ArrayList<>();

        if(nums.length == 0){
            output.add(formatRange(lower, upper));
            return output;
        }
        
        if(nums[0] > lower) {
            output.add(formatRange(lower,nums[0] -1));
        }

        for(int i = 0; i < nums.length - 1; i++) {
            if (nums[i + 1] - nums[i] > 1) {
                output.add(formatRange(nums[i] + 1,nums[i + 1] - 1));
            }
        }

        if (nums[nums.length - 1] < upper) {
            output.add(formatRange(nums[nums.length - 1] + 1, upper));
        }

        return output;
    }

    public static String formatRange (int lower, int upper) {
        if(lower == upper) {
            return String.valueOf(lower);
        } else {
            return lower + "->" + upper;
        }
    }
