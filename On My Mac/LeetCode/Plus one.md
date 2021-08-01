# Plus one

Wrong code:
public static int[] plusOne(int[] digits) {

    if(digits.length == 1 && digits[0] < 9) {
        digits[0] = digits[0] + 1;
         return digits;
    }

    long integer = 0;
    for(int i = 0; i < digits.length; i++) {
        integer += digits[i] * Math.*pow*(10, digits.length - 1 - i);
    }

    integer += 1;
    int newLength = String.*valueOf*(integer).length();
    int[] newDigits = new int[newLength];

    for (int i = 0; i < newLength -1; i++) {
        newDigits[newLength - 1 - i] = (int)integer % 10;
        integer /= 10;
        if(integer < 10) {
            newDigits[0] = (int)integer;
        }
    }

    return newDigits;
}

Correct code:

  public int[] plusOne(int[] digits) {
    int n = digits.length;

    // move along the input array starting from the end
    for (int idx = n - 1; idx >= 0; --idx) {
      // set all the nines at the end of array to zeros
      if (digits[idx] == 9) {
        digits[idx] = 0;
      }
      // here we have the rightmost not-nine
      else {
        // increase this rightmost not-nine by 1
        digits[idx]++;
        // and the job is done
        return digits;
      }
    }
    // we're here because all the digits are nines
    digits = new int[n + 1];
    digits[0] = 1;
    return digits;
  }
