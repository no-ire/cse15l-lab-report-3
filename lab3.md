Name: Calvin Zhou\
Class: cse15l\
Date: 11-19-23

# Lab Report 3

## Part 1: Bugs
a. Failure Inducing Input\
```
@Test
public void testReversedFail() {
  int[] input1 = {1};
  assertArrayEquals(new int[]{1}, ArrayExamples.reversed(input1));
}
```
b. Pass Inducing Input\
```
@Test
public void testReversedPass() {
  int[] input1 = {};
  assertArrayEquals(new int[]{}, ArrayExamples.reversed(input1));
}
```
c. Symptoms
```
There was 1 failure:
1) testReversedFail(ArrayTests)
arrays first differed at element [0]; expected:<1> but was:<0>
at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
at org.junit.Assert.internalArrayEquals(Assert.java:534)
at org.junit.Assert.assertArrayEquals(Assert.java:418)
at org.junit.Assert.assertArrayEquals(Assert.java:429)
at ArrayTests.testReversedFail(ArrayTests.java:21)
... 30 trimmed
Caused by: java.lang.AssertionError: expected:<1> but was:<0>
at org.junit.Assert.fail(Assert.java:89)
at org.junit.Assert.failNotEquals(Assert.java:835)
at org.junit.Assert.assertEquals(Assert.java:120)
at org.junit.Assert.assertEquals(Assert.java:146)
at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.
at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
... 36 more
FAILURES!!!
```
d. Bugs
```
# Before
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = newArray[arr.length - i - 1];
  }
  return arr;
}
```
```
# After
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    newArray[i] = arr[i];
  }
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = newArray[arr.length - i - 1];
  }
  return arr;
}
```
Epxlantion: The second 'for' statement was copying elements from an empty array newArray. So output would always be an empty array.
To fix this, newArray has to be a copy of the original arr, which is why the first 'for' statement is added. 
And now, the second 'for' statment refers to the elements of original arr in reverse order.

## Part 2: Researching Commands
Using the command: Grep
a. Input_1 -i:
```
grep -i "further" biomed/1471-5945-2-13.txt
```
Output_1 -i:
```
Additional data #3). TGFβ1 further induced the expression
outside tension. Furthermore, persisting tension in the
further limited by the PP fibroblast requirement for higher
```
Input_2 -i:
```
grep -i "THEI" biomed/1471-2180-3-5.txt
```
Output_2 -i:
```
induction of TRAIL by Theiler's murine encephalomyelitis
their ability to induce inflammatory responses. The two
```
What and Why?: -i for rep makes case insensitive. It's helpful for when trying to do seraches without worrying about the cases of the letters.

b. Input_1 -c:
```
grep -c " " plos/journal.pbio.0020001.txt
```
Output_2 -c:
```
230
```
Input_2 -c:
```
grep -c "hi" 911report/*.txt
```
Output_2 -c:
```
911report/chapter-1.txt:253
911report/chapter-10.txt:101
911report/chapter-11.txt:179
911report/chapter-12.txt:193
911report/chapter-13.1.txt:132
911report/chapter-13.2.txt:198
911report/chapter-13.3.txt:199
911report/chapter-13.4.txt:603
911report/chapter-13.5.txt:608
911report/chapter-2.txt:232
911report/chapter-3.txt:592
911report/chapter-5.txt:441
911report/chapter-6.txt:351
911report/chapter-7.txt:513
911report/chapter-8.txt:183
911report/chapter-9.txt:373
911report/preface.txt:26
```
What and why?: Used to count lines of string in a file. Useful to find how many lines in a given string.

c. Input_1 -l:
```
grep -l "individual" biomed/1471-210*.txt
```
Output_1 -l:
```
biomed/1471-2105-1-1.txt
biomed/1471-2105-2-1.txt
biomed/1471-2105-2-8.txt
biomed/1471-2105-2-9.txt
biomed/1471-2105-3-12.txt
biomed/1471-2105-3-14.txt
biomed/1471-2105-3-16.txt
biomed/1471-2105-3-17.txt
biomed/1471-2105-3-18.txt
biomed/1471-2105-3-2.txt
biomed/1471-2105-3-22.txt
biomed/1471-2105-3-23.txt
biomed/1471-2105-3-24.txt
biomed/1471-2105-3-26.txt
biomed/1471-2105-3-28.txt
biomed/1471-2105-3-3.txt
biomed/1471-2105-3-30.txt
biomed/1471-2105-3-34.txt
biomed/1471-2105-3-37.txt
biomed/1471-2105-3-38.txt
biomed/1471-2105-3-4.txt
biomed/1471-2105-3-6.txt
biomed/1471-2105-4-13.txt
biomed/1471-2105-4-24.txt
biomed/1471-2105-4-25.txt
biomed/1471-2105-4-26.txt
biomed/1471-2105-4-27.txt
biomed/1471-2105-4-31.txt
```
Input_2 -l:
```
grep -l "government" government/About_LSC/commission_report.txt
```
Output_2 -;:
```
government/About_LSC/commission_report.txt
```
What and why?: Gives name of files. Useful when trying to find file in a string.
