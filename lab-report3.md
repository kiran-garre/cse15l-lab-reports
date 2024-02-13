## Part 1
In this section, I will be focusing on test the `reverseInPlace()` method.
Failure-inducing input (JUnit test):
```
@Test 
public void testReverseInPlaceFail() {
  int[] input1 = {1, 2, 3, 4};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{4, 3, 2, 1}, input1);
}
```
Successful input (JUnit test):
```
@Test
public void testReverseInPlaceSuccess() {
    int[] input1 = {3};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{3}, input1);
}
```
Screenshot of both tests running:
![Image](/lab-report3-images/junit-tests-lab-report3.png)

Before and after:
Before:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
}
```
After:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length / 2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
}
```
The bug in the original code is that the `for` loop iterates through the whole array. The values in the first half of the array are replaced with values from the second half of the array. However, 
the function continues iteratiing through the array and copies the new beginning values (which have already been replaced), which causes the array to be reversed improperly.

## Part 2

In this section, I will be exploring the `grep` command. Since we've already used the `-r` option (which searches the given directory recursively) and the `-l` option (which displays only the filenames),
I will use those without further explanation. I will also use the `head` and `tail` commands to make the output easier to copy and read. 


### `-m` option
Source: `man` page for `grep`
The `-m` option takes a number as an argument and will stop searching after that many matches.
```
separate technical % grep -r -m 5 "the" plos 
plos/pmed.0020273.txt:        Inflammatory bowel disease (IBD) is the term that encompasses chronic relapsing diseases
plos/pmed.0020273.txt:        characterized by inflammation of the bowel, specifically ulcerative colitis (UC) and Crohn
plos/pmed.0020273.txt:        disease (CD). They are common disorders; in the UK, for example, together they affect about
plos/pmed.0020273.txt:        than 1 million cases in the US and Europe. The symptoms for both these conditions—which
plos/pmed.0020273.txt:        suggest an abnormal immune response at the intestinal mucosa—include abdominal pain,
```
In this example, we are searching the `/plos` directory for the string `the`. There are hundreds of lines that contain the string "the", but with the `-m` option and 
by passing 5 as the argument, `grep` only returns the first 5 matches before stopping. 

As another example,
```
separate technical % grep -r "shark" plos
plos/journal.pbio.0020440.txt:        animals. “When you correct for size and temperature, the metabolic rates of a shark, a
plos/journal.pbio.0020276.txt:        also been found in mice, sharks, nematodes, and plants (e.g., Pujol et al. 2001; Nurnberger
plos/journal.pbio.0020113.txt:        and wolf populations brought to the brink of extinction swordfish and sharks are the
plos/journal.pbio.0020113.txt:        more than 90% of large predatory fishes, such as marlin, sharks, and rays.
plos/journal.pbio.0020113.txt:        Despite the controversy, most agree that the large predators, particularly sharks,

separate technical % grep -r -m 3 "shark" plos
plos/journal.pbio.0020440.txt:        animals. “When you correct for size and temperature, the metabolic rates of a shark, a
plos/journal.pbio.0020276.txt:        also been found in mice, sharks, nematodes, and plants (e.g., Pujol et al. 2001; Nurnberger
plos/journal.pbio.0020113.txt:        and wolf populations brought to the brink of extinction swordfish and sharks are the
```
With the first command, we search the `/plos` directory for all instances of the string "shark", and `grep` finds 5 matches. In the next command, we use the `-m` option to limit
the number of matches to 3, and `grep` only returns the first 3 matches before stopping. We can also see that the 3 matches returned by `grep` with the `-m` option are the same 
first 3 matches as without the `-m` option.


### `-v` option
Source: https://docs.rackspace.com/docs/use-the-linux-grep-command
The `-v` option searches for lines without the argument string. 
```
separate technical % grep -m 8 -rv "a" biomed
biomed/1472-6807-2-2.txt:
biomed/1472-6807-2-2.txt:  
biomed/1472-6807-2-2.txt:    
biomed/1472-6807-2-2.txt:      
biomed/1472-6807-2-2.txt:        been developed for the prediction of MHC-peptide binding [
biomed/1472-6807-2-2.txt:        10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 ] .
biomed/1472-6807-2-2.txt:        B *3501, B *5301, H-2K B, H-2D B, H-2D D, H-2L D, DR1, DR2,
biomed/1472-6807-2-2.txt:        improvement in the MHC-peptide binding prediction. [ 21 22
```
In this example, we use the `-v` option with the string "a" (and limit the number of matches to 8 with `-m 8`). We can see that the lines returned by `grep` do not contain the letter "a". The 
3 blank lines at the beginning of the output are empty lines, which do not contain the string "e".

As another example,
```
separate technical % grep -rv "the" plos | tail -n 5        
plos/pmed.0020242.txt:        should be commended for addressing an extremely important issue and developing this novel
plos/pmed.0020242.txt:        approach for counting CD4 in patients with HIV.”
plos/pmed.0020242.txt:      
plos/pmed.0020242.txt:    
plos/pmed.0020242.txt:  
```
We can see that the `-v` option once again returns lines without the argument, which in this case is the word "the" (the `tail` command is used for readability and variety). The blank lines are 
empty lines that also do not contain the string "the". 



### `-n` option
Source: `man` page for `grep`
The `-n` option prints the line number corresponding to each match that grep finds.
```
separate technical % grep -r -n "dna" biomed | head -n 5 
biomed/gb-2002-4-1-r2.txt:302:          (SCY). Uroldnase and uroldnase receptors were both
biomed/1471-2091-2-13.txt:518:          http://combdna.umbi.umd.edu/bags.html. The aligned small
biomed/1471-2180-1-12.txt:6:        Hepadnaviruses are small, enveloped hepatotropic viruses
biomed/1471-2180-1-12.txt:9:        of hepadnaviral DNA is initiated by the interaction of the
biomed/1471-2180-1-12.txt:27:        The hepadnaviral P protein possesses many unique
```
We can see that now, the file path printed with each match ends with the line number of each file where the match is found. For example, we see that 
the string "dna" is found on line 302 of the file `biomed/gb-2002-4-1-r2.txt`. 

The `-n` option can also be combined with other options:
```
separate technical % grep -rv -n "a" biomed | head -n 8
biomed/1472-6807-2-2.txt:1:
biomed/1472-6807-2-2.txt:2:  
biomed/1472-6807-2-2.txt:3:    
biomed/1472-6807-2-2.txt:4:      
biomed/1472-6807-2-2.txt:36:        been developed for the prediction of MHC-peptide binding [
biomed/1472-6807-2-2.txt:37:        10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 ] .
biomed/1472-6807-2-2.txt:61:        B *3501, B *5301, H-2K B, H-2D B, H-2D D, H-2L D, DR1, DR2,
biomed/1472-6807-2-2.txt:78:        improvement in the MHC-peptide binding prediction. [ 21 22
```
Here, we search for lines that do not contain a match to the string "a" using the `-v` option. Including the `-n` option still returns the line numbers of the
lines returned by grep, as expected. 

### `-w` option
Source: https://docs.rackspace.com/docs/use-the-linux-grep-command
The `-w` option only matches the argument string as a word, not as pard of another word. For example, passing "cat" as an argument to `grep` with the `-w` function would
only match the word "cat" and not the word "catastrophe".
```
separate technical % grep -r "a" plos | head -n 5      
plos/pmed.0020273.txt:        Inflammatory bowel disease (IBD) is the term that encompasses chronic relapsing diseases
plos/pmed.0020273.txt:        characterized by inflammation of the bowel, specifically ulcerative colitis (UC) and Crohn
plos/pmed.0020273.txt:        disease (CD). They are common disorders; in the UK, for example, together they affect about
plos/pmed.0020273.txt:        one person in every 400, amounting to a total of 120,000 cases of UC and 60,000 of CD, with
plos/pmed.0020273.txt:        6,000 new cases of UC and 3,000 new cases of CD every year. Current estimates total at more

separate technical % grep -r -w "a" plos | head -n 5
plos/pmed.0020273.txt:        one person in every 400, amounting to a total of 120,000 cases of UC and 60,000 of CD, with
plos/pmed.0020273.txt:        pathogenesis suggests a complex action of multiple environmental factors that trigger
plos/pmed.0020273.txt:        disease in individuals with a susceptible genetic background.
plos/pmed.0020273.txt:        Today, finding genes that have a role in diseases has been made easier by the sequencing
plos/pmed.0020273.txt:        variants with a causative role. Another of the tools for analyzing genes is microarray
```
With the first command, we can see that passing "a" as an argument to `grep` without the `-w` option returns several lines that contain "a" (only 5 are displayed because of the `head` command). 
In the second command, we use the `-w` option, and we see that the difference is that these lines contain "a" as a word, not as a part of another word. 

As another example,
```
separate technical % grep -r "cat" plos | head -n 5 
plos/pmed.0020273.txt:        Ultimately this study highlights the complex pathogenesis of UC and CD, and indicates
plos/journal.pbio.0030032.txt:        worldwide gold standard for science education—is too specialized for their needs (see Box
plos/journal.pbio.0030032.txt:        many fields, including business, education, and social work, and more recently, pharmacy,
plos/journal.pbio.0030032.txt:        communication, with authentic case studies analyzed alongside MBA students, classroom
plos/journal.pbio.0030032.txt:        the presence of a central employee who streams data between differently educated members of

separate technical % grep -r -w "cat" plos | head -n 5
plos/journal.pbio.0020146.txt:        nerve fibers in the rat and cat and some 25,000–30,000 in the human (cf. Hall and Masengill
plos/pmed.0020034.txt:        to inadequate exposure, since all estimates of the quantity of cat allergen inhaled are
plos/pmed.0020034.txt:        higher than for dust mites. Furthermore, the quantity of cat allergen found in schools or
plos/pmed.0020034.txt:        In fact, children raised in a house with a cat were less likely to be sensitized to cats
plos/pmed.0020034.txt:        keep cats, and very few families report choosing not to own a cat because of asthma in the
```
In the first command, `grep` returns several lines that contain the string "cat", even if "cat" is contained in other words like "indicates" and "education".
In the second command, `grep` with the `-w` option only returns matches where "cat" is a standalone word.


  
