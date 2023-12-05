# Part 1 - Debugging Scenario

1. **Student Post:**

Hi,

I'm currently having issues with running a `reversed` method that is supposed to return an array with all the elements of the input array in reversed order. When running the ArrayExamples.java file with JUnit tests, the expected output was a reversed input list of `{1,2,3,4}` which should be `{4,3,2,1}` but was actually throwing an Out of Bounds Exception showing that the method is incorrect. I'm not sure what is incorrect but my guess is that I'm sorting using the current array and therefore reusing values that had already been sorted at a certain index. The images below display the incorrect reversed method and the symptom.

Incorrect `reversed` method:
![Screenshot 2023-12-04 193849](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/da998fde-64ed-4942-9c6c-4fcd8b878579)

Symptom for failure-inducing input:
![Screenshot 2023-12-04 200345](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/4c5cc5e4-e1ad-4709-8a30-d887b996d5d9)

2. **TA Response:**

Hello,

In your incorrect `reversed` method, recheck the loop conditions that don't seem to be correct causing the Out of Bounds Exception. It also seems the code is incorrectly assigning values from the uninitialized `newArray` to the input array `arr`. Instead of returning the original input array `arr` again, what could you do to return the new array `newArray` instead? I also recommend you print out which numbers you are swapping to observe if the method is correctly reversing them.

3. **Student Corrected Output:**

Hi,

Thanks for your help! I realized the bug was that I put an `=` inside the for-loop causing the loop to attempt an out-of-bounds access. I also was essentially copying values from `newArray` to `arr`, but in the wrong order. This overwrites the values of `arr` with uninitialized values from `newArray` and therefore the incorrect, uninitialized values are being returned. I also added code to print what values were being correctly swapped and the right code and output are below.

Corrected `reversed` method:
![Screenshot 2023-12-03 153538](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/1ba287c8-3359-413b-af95-e19720fda56b)

Terminal output:

![Screenshot 2023-12-04 194343](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/7f61ff0e-4fef-4873-b924-e3c7d1eb2108)

4. **All information needed about the setup**

   1. The file & directory structure needed
  
        Commands: Log into ieng6 account as a CSE15L student with the command `ssh cs15lfa23ea@ieng6.ucsd.edu`.
                  Git clone the `lab3` repository with the command `git clone git@github.com:clarissacheng/lab3.git`.
                  Access `lab3` directory with `cd lab3`. I had my incorrect `reversed` method within the ArrayExamples.java file.
      		  The ArrayTests.java file tested the `reversed` method. The test.sh file contained the commands to run the JUnit tests that would run the ArrayTests.java file. 
![Screenshot 2023-12-04 200247](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/679c4fb7-0f20-4421-896f-8ce1e3af1d63)
      
   2.The contents of each file before fixing the bug

`ArrayExamples.java`

```
public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i <= arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }

  // Averages the numbers in the array (takes the mean), but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }
}
```

`ArrayTests.java`

```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
  @Test
  public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
  }

  @Test
  public void testReversed() {
    int[] input1 = {1,2,3,4};
    assertArrayEquals(new int[]{4,3,2,1}, ArrayExamples.reversed(input1));
  }
}                                                                      
```

`test.sh`
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
```
      
   3. The full command line (or lines) you ran to trigger the bug

      Commands: `bash test.sh`

      `test.sh` contains: 
![Screenshot 2023-12-04 200606](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/e9fe9b86-fff3-45da-87b6-a86733216109)

  5. A description of what to edit to fix the bug

     To fix the bug, we must first delete the `=` within the for-loop because this would cause an out-of-bounds exception where we try to access an element using an index that is outside the valid range of indices for that array. We also must populate the `newArray` with the reversed values from the input array `arr`. The original reversed method incorrectly reverses the input array because it assigns uninitialized `newArray` to the `arr` array which results in incorrect output. To fix this, I switch `arr` for `newArray` and input this array with the reversed values from input array `arr`. This ensures the `newArray` contains the reversed values and that the reversed array is returned.
     Within the for loop of the `reversed` method, I also wrote a print statement that will output which values are being reversed between the two arrays just as the TA suggested.

# Part 2 - Reflection

Something that I learned from lab experience and enjoyed was VIM. I think it was fun to learn about how to do everything from the command line, even editing files using VIM, and all the special keys to make those edits. Racing my classmates and trying to beat my own time made learning VIM fun and I enjoyed using it for the following labs as well. 
