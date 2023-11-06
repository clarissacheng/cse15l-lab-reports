# Part 1 - Bugs

The bug I chose is the reversed method from the ArrayExamples.java file. 

* A failure-inducing input for the buggy program
```
@Test
  public void testReversed2() {
    int[] input1 = {1,2,3,4};
    assertArrayEquals(new int[]{4,3,2,1}, ArrayExamples.reversed(input1)); //array first differed at element [0]; expected <4> but was <0>
  }
```
* An input that doesn’t induce a failure
```
@Test
  public void testReversed2() {
    int[] input1 = {};
    assertArrayEquals(new int[]{}, ArrayExamples.reversed(input1)); //no input so no error as nothing is incorrectly reversed
  }
```
* The symptom for the failure-inducing input
```
JUnit version 4.13.2
....E
Time: 0.016
There was 1 failure:
1) testReversed2(ArrayTests)
arrays first differed at element [0]; expected:<4> but was:<0>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReversed2(ArrayTests.java:28)
        ... 32 trimmed
Caused by: java.lang.AssertionError: expected:<4> but was:<0>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 38 more

FAILURES!!!
Tests run: 4,  Failures: 1
```
* The symptom for the input that doesn’t induce a failure
```
JUnit version 4.13.2
....
Time: 0.01

OK (4 tests)
```
* Bug before
```
  // Returns a *new* array with all the elements of the input array in reversed order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
* Bug fixed
```
  // Returns a *new* array with all the elements of the input array in reversed order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```
* The original `reversed` method incorrectly reverses the input array because it assigns uninitialized `newArray` to the  `arr` array which results in incorrect output.
To fix this, I switch `arr` for  `newArray` and input this array with the reversed values from input array `arr`. This ensures the `newArray` contains the reversed values and that the reversed array is returned.

# Part 2 - Researching Commands

## 1. grep -i
```
grep -i "activities" ./technical/911report/chapter-13.1.txt
                    locations to coordinate the activities of other agencies when action may be
                    be responsible for being sure that intelligence gathered from the activities in
                the activities of other agencies. Law or executive order must define the scope of
                    create a group of professionals better able to operate in joint activities,
                    intelligence program (JMIP) and the tactical intelligence and related activities
                Congress have the broad knowledge of intelligence activities or the know-how about
                    activities of the intelligence agencies and report problems relating to the
```
* This command line searches for the pattern "activities" in the `chapter-13.1.txt` file and ignores any capitalizations of "activities". Source: https://en.wikibooks.org/wiki/Grep
```
grep -i "breathe" ./technical/*/*.txt
./technical/911report/chapter-1.txt:    At 8:19, Ong reported:"The cockpit is not answering, somebody's stabbed in business class-and I think there's Mace-that we can't breathe-I don't know, I think we're getting hijacked." She then told of the stabbings of the two flight attendants.
./technical/911report/chapter-13.5.txt:                Administrator Christine Whitman as saying that the air was "safe" to breathe. This
./technical/911report/chapter-13.5.txt:                controversial release that specifically declared the air safe to breathe was 
./technical/911report/chapter-9.txt:                impossible to breathe. This person escaped by means of an unlikely rescue, aided by
./technical/biomed/1476-069X-1-3.txt:          the amount of air that has been previously breathed by
./technical/biomed/1476-069X-1-3.txt:          building occupants. Rebreathed air potentially contains
./technical/biomed/1476-069X-2-9.txt:            while they may breathe in the water vapor above the
./technical/biomed/1477-7827-1-43.txt:        Lifr genotypes are able to breathe
./technical/biomed/cc1495.txt:        During the study all patients breathed room air, and
./technical/biomed/cc1856.txt:          Duluth, CA, USA). Rats breathed room air, spontaneously,
./technical/plos/pmed.0020281.txt:        redeemed social condition; to know even one life breathed easier because you have lived;
```
* This command line searches for the pattern "breathe" in all `.txt` files in the `./technical` directory and this is useful because it performs a case-insensitive search denoted by the `-i`. Source: https://en.wikibooks.org/wiki/Grep

## 2. grep -r
```
grep -r "scope" ./technical/911report/chapter-13.1.txt
                the activities of other agencies. Law or executive order must define the scope of
```
* This commmand line recursively searches for the pattern "scope" in the `chapter-13.1.txt` file and this is useful because we don't need exact file paths, but in this case, I still only refer to one file. Source: https://en.wikibooks.org/wiki/Grep
```
grep -rn "breathe" ./technical/*/*.txt
./technical/911report/chapter-1.txt:76:    At 8:19, Ong reported:"The cockpit is not answering, somebody's stabbed in business class-and I think there's Mace-that we can't breathe-I don't know, I think we're getting hijacked." She then told of the stabbings of the two flight attendants.
./technical/911report/chapter-13.5.txt:2288:                Administrator Christine Whitman as saying that the air was "safe" to breathe. This
./technical/911report/chapter-13.5.txt:2330:                controversial release that specifically declared the air safe to breathe was
./technical/911report/chapter-9.txt:654:                impossible to breathe. This person escaped by means of an unlikely rescue, aided by
./technical/biomed/1476-069X-1-3.txt:172:          the amount of air that has been previously breathed by
./technical/biomed/1476-069X-1-3.txt:173:          building occupants. Rebreathed air potentially contains
./technical/biomed/1476-069X-2-9.txt:493:            while they may breathe in the water vapor above the
./technical/biomed/1477-7827-1-43.txt:680:        Lifr genotypes are able to breathe
./technical/biomed/cc1495.txt:84:        During the study all patients breathed room air, and
./technical/biomed/cc1856.txt:100:          Duluth, CA, USA). Rats breathed room air, spontaneously,
./technical/plos/pmed.0020281.txt:36:        redeemed social condition; to know even one life breathed easier because you have lived;
```
* This command line recursively searches for the pattern "breathe" in the `./technical` directory and this is useful because it searches in all files under the directory and also shows the line numbers for matches. Source: https://en.wikibooks.org/wiki/Grep

## 3. grep -C 
```
grep -C 2 "dangers" ./technical/911report/preface.txt
                between and within agencies. We learned of the pervasive problems of managing and
                sharing information across a large and unwieldy government that had been built in a
                different era to confront different dangers.
            At the outset of our work, we said we were looking backward in order to look forward.
                We hope that the terrible losses chronicled in this report can create something
```
* This command line displays the number of lines and its context before and after each match. We are presented the 2 lines before and after the match "dangers". This is helpful because we can find the context around certain words or matches. Source: https://www.ibm.com/docs/sk/aix/7.1?topic=g-grep-command
```
grep -C 1 "moon" ./technical/*/*.txt
./technical/911report/chapter-6.txt-                pulled Musharraf aside for a brief, one-on-one meeting, he pleaded with the general
./technical/911report/chapter-6.txt:                for help regarding Bin Ladin." I offered him the moon when I went to see him, in    
./technical/911report/chapter-6.txt-                terms of better relations with the United States, if he'd help us get Bin Ladin and 
--
./technical/biomed/1471-213X-1-6.txt-          visible in the dorsal fin fold. Although the pectoral fin
./technical/biomed/1471-213X-1-6.txt:          has acquired the shape of a half-moon, it still has no
./technical/biomed/1471-213X-1-6.txt-          flange. Gill filaments are sprouting on branchial arches
--
./technical/biomed/1471-213X-1-6.txt-          its fin folds. The pectoral fin is larger than a
./technical/biomed/1471-213X-1-6.txt:          half-moon, with a flange narrower than its muscle mass.
./technical/biomed/1471-213X-1-6.txt-          The operculum is nearly twice as wide as the eye. Gill
--
./technical/biomed/1471-213X-1-6.txt-          (Fig. 9E, 9F) - The yolk is finally exhausted. Pelvic
./technical/biomed/1471-213X-1-6.txt:          fins are half-moon shaped with narrow membranous flanges.
./technical/biomed/1471-213X-1-6.txt-          The jaws are studded with sharp teeth.
--
./technical/biomed/gb-2002-3-5-research0025.txt-          lineages. This might occur if the protein has a second
./technical/biomed/gb-2002-3-5-research0025.txt:          function (a 'moonlighting' function) in some lineages and
./technical/biomed/gb-2002-3-5-research0025.txt-          is subject to selective pressure that alters regions of
--
./technical/biomed/gb-2003-4-5-r32.txt-          vector element before comparison with the neural network.
./technical/biomed/gb-2003-4-5-r32.txt:          For example, nuclei with a 'half-moon' silhouette caused
./technical/biomed/gb-2003-4-5-r32.txt-          by the sectioning process will be misleading. In this
--
./technical/plos/journal.pbio.0020302.txt-        concretions. The case for water, we could say, is tight.
./technical/plos/journal.pbio.0020302.txt:        On Jupiter's moon Europa, the cracks and icebergs on the surface of the ice indicate  
./technical/plos/journal.pbio.0020302.txt-        water beneath the ice, but not necessarily at the present time. Present water on Europa is
--
./technical/plos/journal.pbio.0020439.txt-        believed to ebb and flow under the motive power of the liver, just as the tides of the
./technical/plos/journal.pbio.0020439.txt:        earth ebbed and flowed under the motive power of the moon. Harvey became physician to the
./technical/plos/journal.pbio.0020439.txt-        king of England. He used his position of privilege to dissect deer from the king's deer
```
* This command line displays the number of lines and its context before and after each match. We are presented the 1 line before and after the match "moon". This is helpful because we can find the context around certain words or matches. Source: https://www.ibm.com/docs/sk/aix/7.1?topic=g-grep-command

## 4. grep -l
```
grep -l "losses" ./technical/911report/preface.txt
./technical/911report/preface.txt
```
* This command line lists the name of files containing the specified word "losses" and since "losses" is found in the file, only the file is listed. This is useful because we can find which files contain the specific word. Source: https://en.wikibooks.org/wiki/Grep
```
grep -l "preface" ./technical/*/*.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
````
* This command line lists the name of the files containing the specified word "preface" and the word was found within those listed files. This is useful because we can find which files contain the specific word. Source: https://en.wikibooks.org/wiki/Grep
