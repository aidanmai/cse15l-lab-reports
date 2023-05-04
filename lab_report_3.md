# Lab Report 3

Chosen command: `grep`

Source for all command options: [https://man7.org/linux/man-pages/man1/grep.1.html](https://man7.org/linux/man-pages/man1/grep.1.html)

**Option 1:** `-m`

The `-m` option allows you to limit the number of matching lines outputted from the `grep` command. This is useful if you only want the first X matching lines from each file.

This command searches for the first instance of "deoxyribonucleic" in each file in `plos`.
```
grep -m 1 "deoxyribonucleic" biomed/*.txt
biomed/1471-2164-3-7.txt:        - deoxyribonucleic acid, PBS - phosphate buffer saline, DEX
biomed/1471-2350-3-12.txt:        cDNA complementary deoxyribonucleic acid
biomed/ar130.txt:          complementary deoxyribonucleic acids (cDNAs) [ 11].
biomed/gb-2003-4-9-r60.txt:        biochips including complementary deoxyribonucleic acid
```

This command searches for the first instance of "base pair" in each file in `plos`.
```
grep -m 2 "base pair" plos/*.txt
plos/journal.pbio.0020190.txt:        sequence, which is a specific series of eight base pairs in the DNA of the bacterial
plos/journal.pbio.0020190.txt:        chromosomes, on the order of one or two thousand base pairs of DNA (or less—their length is
plos/journal.pbio.0020223.txt:        Watson-Crick base pairing, the proximity of the synthetic reactive groups elevates their
```

**Option 2:** `-E`

The `-E` option allows the match string to be interpreted as a regular expression, which is useful if you want to use regex to be very specific about what you're searching for.

This command searches for all 10-digit or longer numbers in the `biomed` directory.
```
grep -E "\d{10,}" biomed/*.txt
biomed/gb-2002-3-12-research0085.txt:          genes. WGS3 scaffold 211000022279294 contains rDNA
biomed/gb-2002-4-1-r1.txt:            predicted transcript ENST00000299272, we found a mouse
```

This command searches for all words 80 letters or longer in the `biomed` directory.
```
grep -E "\w{80,}" */*.txt
biomed/1471-2121-4-3.txt:          (5'-gatcCTCGAGatcgataccgtcgagctagcgtagtctgggacgtcgtatgggtatcgactcatATTCGAGATATTTGATTATACCAAGGC-3').
biomed/1471-2156-3-17.txt:          (5'-GATCCAATTGAAAAGTACGTTAAGAACAGCGGCAATAATTTGGGGATTTGTTTCTACAAAGAAGCTGCGATGAGTAAAGGAGAAGAACTT-3')
biomed/1471-2156-4-6.txt:          TATTTTCTCACTACAGAATTGTTGGAAGTTTGCGTCTCTCCCGAAGAGCTGGAGCAGTTGTACACTAATTTTCGGATCCCCGGGTTAATTAA;
biomed/1471-2156-4-6.txt:          GATGTGGGTGCGGGACGGGAAAGAACAACACTGAAGAAACAAGTATCATTATTTCATTTGAAAAATTAGGGAAATGAATTCGAGCTCGTTTAAAC)
```

**Option 3:** `-o`

The `-o` option allows you to only output the exact matching strings, not the rest of the line. This is probably most useful if you're using regex in conjunction with the `E` option and want to extract only matching strings from files for further processing.

This command searches for all 10-digit or longer numbers in the `biomed` directory, omitting the rest of the line.
```
grep -E -o "\d{10,}" */*.txt
biomed/gb-2002-3-12-research0085.txt:211000022279294
biomed/gb-2002-4-1-r1.txt:00000299272
```

This command searches for all words 80 letters or longer in the `biomed` directory, omitting the rest of the line.
```
grep -E -o "\w{80,}" */*.txt
biomed/1471-2121-4-3.txt:gatcCTCGAGatcgataccgtcgagctagcgtagtctgggacgtcgtatgggtatcgactcatATTCGAGATATTTGATTATACCAAGGC
biomed/1471-2156-3-17.txt:GATCCAATTGAAAAGTACGTTAAGAACAGCGGCAATAATTTGGGGATTTGTTTCTACAAAGAAGCTGCGATGAGTAAAGGAGAAGAACTT
biomed/1471-2156-4-6.txt:TATTTTCTCACTACAGAATTGTTGGAAGTTTGCGTCTCTCCCGAAGAGCTGGAGCAGTTGTACACTAATTTTCGGATCCCCGGGTTAATTAA
biomed/1471-2156-4-6.txt:GATGTGGGTGCGGGACGGGAAAGAACAACACTGAAGAAACAAGTATCATTATTTCATTTGAAAAATTAGGGAAATGAATTCGAGCTCGTTTAAAC
```

**Option 4:** `h`

The `h` command omits filenames from output. This is most useful if you don't care about where the matching strings came from, and need to get rid of the filenames before further processing.

This command searches for all 10-digit or longer numbers in the `biomed` directory, omitting the filename and the rest of the line.
```
grep -E -o -h "\d{10,}" */*.txt 
211000022279294
00000299272
```

This command searches for all words 80 letters or longer in the `biomed` directory, omitting the filename and the rest of the line.
```
grep -E -o -h "\w{80,}" */*.txt
gatcCTCGAGatcgataccgtcgagctagcgtagtctgggacgtcgtatgggtatcgactcatATTCGAGATATTTGATTATACCAAGGC
GATCCAATTGAAAAGTACGTTAAGAACAGCGGCAATAATTTGGGGATTTGTTTCTACAAAGAAGCTGCGATGAGTAAAGGAGAAGAACTT
TATTTTCTCACTACAGAATTGTTGGAAGTTTGCGTCTCTCCCGAAGAGCTGGAGCAGTTGTACACTAATTTTCGGATCCCCGGGTTAATTAA
GATGTGGGTGCGGGACGGGAAAGAACAACACTGAAGAAACAAGTATCATTATTTCATTTGAAAAATTAGGGAAATGAATTCGAGCTCGTTTAAAC
```
