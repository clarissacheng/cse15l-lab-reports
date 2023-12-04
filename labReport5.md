# Part 1 - Debugging Scenario

1. **Student Post:**

Hi,

I'm currently having issues with running a `reversed` method that is supposed to return an array with all the elements of the input array in reversed order. When running the ArrayExamples.java file with JUnit tests, the expected output was <4> but was actually <0> showing that the method is incorrect. I'm not sure what is incorrect but my guess is that I'm sorting using the current array and therefore reusing values that had already been sorted at a certain index. The images below display the incorrect reversed method and the symptom.

Incorrect `reversed` method:
![CSE15Lab5pic1](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/3b841a30-4d78-46e4-9de2-2cc13c6e37b2)

Symptom for failure-inducing input:
![Screenshot 2023-12-03 144645](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/7b7a8a54-f3d7-4ba7-8ecd-c83f23ce998f)

2. **TA Response:**

Hello,

In your incorrect method, it seems that the code is incorrectly assigning values from the uninitialized `newArray` to the input array `arr`. Instead of returning the original input array `arr` again, what could you do to return the new array `newArray` instead? I also recommend you print out which numbers you are swapping to observe if the method is correctly reversing them.

3. **Student Corrected Output:**

Hi,

Thanks for your help! I realized the bug was that I was essentially copying values from `newArray` to `arr`, but in the wrong order. This overwrites the values of `arr` with uninitialized values from `newArray` and therefore the incorrect, uninitialized values are being returned. I also added code to print what values were being correctly swapped and the right code and output is below.

Corrected `reversed` method:
![Screenshot 2023-12-03 153538](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/1ba287c8-3359-413b-af95-e19720fda56b)

Terminal output:

![Screenshot 2023-12-03 153122](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/615130b5-59bf-48f8-b8e9-84fb488ba493)

4. **All information needed about the setup**

   1. The file & directory structure needed
  
        Commands: Log into ieng6 account as a CSE15L student with the command `ssh cs15lfa23ea@ieng6.ucsd.edu`.
                  Git clone the `lab3` repository with the command `git clone git@github.com:clarissacheng/lab3.git`.
                  Access `lab3` directory with `cd lab3`.
      
        Keys pressed:
      ```
      <s><s><h><space><c><s><1><5><l><f><a><2><3><e><a><@>
      <i><e><n><g><6><.><u><c><s><d><.><e><d><u><enter>




      
      	<g> <i> <t> <space> <c> <l> <o> <n> <e> <space> <ctrl-v> <enter>




      
      	<c> <d> <space> <l> <a> <b> <3> <enter>
      ```
      
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
    for(int i = 0; i < arr.length; i += 1) {
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
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }

  @Test
  public void testReverseInPlace2() {
    int[] input1 = {1,2,3,4};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{4,3,2,1}, input1); //array first differed at element [2]; expected <2> but was <3>
  }

  @Test
  public void testReversed2() {
    int[] input1 = {1,2,3,4};
    assertArrayEquals(new int[]{4,3,2,1}, ArrayExamples.reversed(input1)); //array first differed at element [0];
    expected <4> but was <0>
  }
}
```
      
   3. The full command line (or lines) you ran to trigger the bug

      Commands: I ran the bash script `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar` command but since I ran it 7 lines before I used short cut arrows which are seen below in the Keys Pressed section.
                I ran the bash script `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests` command but since I ran it 7 lines before I used short cut arrows which is seen below in the Keys Pressed section.
                Both of these commands are required to run the JUnit tests to trigger the bug in the code.
      
        Keys pressed: 
      ```
      <up> <up> <up> <up> <up> <up> <up> <Enter>
      <up> <up> <up> <up> <up> <up> <up> <Enter>
      ```

  4. A description of what to edit to fix the bug

     To fix the bug, we must populate the `newArray` with the reversed values from the input array `arr`. The original reversed method incorrectly reverses the input array because it assigns uninitialized `newArray` to the `arr` array which results in incorrect output. To fix this, I switch `arr` for `newArray` and input this array with the reversed values from input array `arr`. This ensures the `newArray` contains the reversed values and that the reversed array is returned.
     Within the for loop of the `reversed` method, I also wrote a print statement that will output which values are being reversed between the two arrays just as the TA suggested.

# Part 2 - Reflection

Something that I learned from lab experience and enjoyed was VIM. I think it was fun to learn about how to do everything from the command line, even editing files using VIM, and all the special keys to make those edits. Racing my classmates and trying to beat my own time made learning VIM fun and I enjoyed using it for the following labs as well. 
