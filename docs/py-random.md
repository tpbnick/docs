# Random Programs

## Cash
In `cash.py` we will calculate the minimum number of coins required to give a user change.  

Ex:
```
$ python cash.py
Change owed: 0.41
4
```

We will first ask a user how much changed they are owed and then tell them the minimum number of coins (.25, .10, .05, and .01) with which said change can be made.  

We will utilized `get_float` from the CS50 library to get the user's input and `print` to output the answer.  

Remember, if the user provides a non-negative value, our program should reprompt the user for a valid amount again and again until the user complies.  

```py linenums="1"
from cs50 import get_float

while True:
	dollars = get_float("Change owed: ")
	if dollars >= 0:
		break

cents = int(dollars * 100)

total_coins = 0

for coin in [25, 10, 5, 1]:
	total_coins += cents // coin
	cents %= coin

print(total_coins)
```

## Readability
In `readability.py` we will compute the approximate grade level of given text.  

Ex:
```
$ python readability.py
Text: Congratulations! Today is your day. You're off to Great Places! You're off and away!
Grade 3
```
This is a complete copy of [`readbility.c`](https://docs.nicklyss.com/c-arrays/#reading-levels-program), which uses the Coleman-Liau index to output grade level from text, but created using Python.  

```py linenums="1"
from cs50 import get_string

text = get_string("Text: ")

letters = sentences = words = 0

for char in text:
	if char.isalpha():
		letters += 1
	if char.isspace():
		words += 1
	if char in ['?', '!', '.']:
		sentences += 1

words += 1
L = (letters * 100) / words
S = (sentences * 100) / words

result = int(round(0.0588 * L - 0.296 * S - 15.8))

if result < 1:
	print("Before Grade 1")
elif result >= 16:
	print("Grade 16+")
else:
	print(f"Grade {result}")
```

### DNA
In this `dna.py` we will identify a person based on their DNA.  

DNA, the carrier of genetic information in living things, has been used in criminal justice for decades. But how, exactly, does DNA profiling work? Given a sequence of DNA, how can forensic investigators identify to whom it belongs?  

Well, DNA is really just a sequence of molecules called nucleotides, arranged into a particular shape (a double helix). Each nucleotide of DNA contains one of four different bases: adenine (A), cytosine (C), guanine (G), or thymine (T). Every human cell has billions of these nucleotides arranged in sequence. Some portions of this sequence (i.e. genome) are the same, or at least very similar, across almost all humans, but other portions of the sequence have a higher genetic diversity and thus vary more across the population.  

One place where DNA tends to have high genetic diversity is in Short Tandem Repeats (STRs). An STR is a short sequence of DNA bases that tends to repeat consecutively numerous times at specific locations inside of a person’s DNA. The number of times any particular STR repeats varies a lot among individuals. In the DNA samples below, for example, Alice has the STR `AGAT` repeated four times in her DNA, while Bob has the same STR repeated five times.

|        |    |                       |                       |                       |                       |                       |   |   |
|--------|----|-----------------------|-----------------------|-----------------------|-----------------------|-----------------------|---|---|
| Alice: | CT | <strong>AGAT</strong> | <strong>AGAT</strong> | <strong>AGAT</strong> | <strong>AGAT</strong> | GACT                  | A |   |
| Bob:   | CT | <strong>AGAT</strong> | <strong>AGAT</strong> | <strong>AGAT</strong> | <strong>AGAT</strong> | <strong>AGAT</strong> | T |   |  

Using multiple STRs, rather than just one, can improve the accuracy of DNA profiling. If the probability that two people have the same number of repeats for a single STR is 5%, and the analyst looks at 10 different STRs, then the probability that two DNA samples match purely by chance is about 1 in 1 quadrillion (assuming all STRs are independent of each other). So if two DNA samples match in the number of repeats for each of the STRs, the analyst can be pretty confident they came from the same person. CODIS, The [FBI’s DNA database](https://www.fbi.gov/services/laboratory/biometric-analysis/codis/codis-and-ndis-fact-sheet), uses 20 different STRs as part of its DNA profiling process.  

What might such a DNA database look like? Well, in its simplest form, you could imagine formatting a DNA database as a CSV file, wherein each row corresponds to an individual, and each column corresponds to a particular STR.

```
name,AGAT,AATG,TATC
Alice,28,42,14
Bob,17,22,19
Charlie,36,18,25
```
The data in the above file would suggest that Alice has the sequence `AGAT` repeated 28 times consecutively somewhere in her DNA, the sequence `AATG` repeated 42 times, and `TATC` repeated 14 times. Bob, meanwhile, has those same three STRs repeated 17 times, 22 times, and 19 times, respectively. And Charlie has those same three STRs repeated 36, 18, and 25 times, respectively.  

So given a sequence of DNA, how might you identify to whom it belongs? Well, imagine that you looked through the DNA sequence for the longest consecutive sequence of repeated `AGAT`s and found that the longest sequence was 17 repeats long. If you then found that the longest sequence of `AATG` is 22 repeats long, and the longest sequence of `TATC` is 19 repeats long, that would provide pretty good evidence that the DNA was Bob’s. Of course, it’s also possible that once you take the counts for each of the STRs, it doesn’t match anyone in your DNA database, in which case you have no match.  

In practice, since analysts know on which chromosome and at which location in the DNA an STR will be found, they can localize their search to just a narrow section of DNA. But we’ll ignore that detail for this problem.  

[.zip file for CSV](https://cdn.cs50.net/2019/fall/psets/6/dna/dna.zip).

```py linenums="1"
from csv import reader, DictReader
from sys import argv

if len(argv) < 3:
    print("usage error, dna.py sequence.txt database.csv")
    exit()

# read the dna sequence from the file
with open(argv[2]) as dnafile:
    dnareader = reader(dnafile)
    for row in dnareader:
        dnalist = row

# store it in a string
dna = dnalist[0]
# create a dictionary where we will store the sequences we intend to count
sequences = {}

# extract the sequences from the database into a list
with open(argv[1]) as peoplefile:
    people = reader(peoplefile)
    for row in people:
        dnaSequences = row
        dnaSequences.pop(0)
        break

# copy the list in a dictionary where the genes are the keys
for item in dnaSequences:
    sequences[item] = 1

# iterate trough the dna sequence, when it finds repetitions of the values from sequence dictionary it counts them
for key in sequences:
    l = len(key)
    tempMax = 0
    temp = 0
    for i in range(len(dna)):
        # after having counted a sequence it skips at the end of it to avoid counting again
        while temp > 0:
            temp -= 1
            continue

        # if the segment of dna corresponds to the key and there is a repetition of it we start counting
        if dna[i: i + l] == key:
            while dna[i - l: i] == dna[i: i + l]:
                temp += 1
                i += l

            # it compares the value to the previous longest sequence and if it is longer it overrides it
            if temp > tempMax:
                tempMax = temp

    # store the longest sequences in the dictionary using the correspondent key
    sequences[key] += tempMax

# open and iterate trough the database of people treating each one like a dictionary so it can compare to the sequences one
with open(argv[1], newline='') as peoplefile:
    people = DictReader(peoplefile)
    for person in people:
        match = 0
        # compares the sequences to every person and prints name before leaving the program if there is a match
        for dna in sequences:
            if sequences[dna] == int(person[dna]):
                match += 1
        if match == len(sequences):
            print(person['name'])
            exit()

    print("No match")
```