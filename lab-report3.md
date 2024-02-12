## Part 2

In this section, I will be exploring the `grep` command. Since we've already used the `-r` option (which searches the given directory recursively) and the `-l` option (which displays only the filenames),
I will use those without further explanation. I will also use the `head` and `tail` commands to make the output easier to copy and read. 


### `-m` option
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



###`-L` option
The `-L` option is similar to the `-v` option, but it only lists the distinct filenames that do not contain the string passed as an argument.
```

* `-w` option



  
