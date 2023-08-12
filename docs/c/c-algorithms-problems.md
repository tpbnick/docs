# Algorithm Problems

## Plurality Problem

Now let's take our new knowledge of algorithms and create a program that runs a
plurality election that will yield the following output:

```
$ ./plurality Alice Bob Charlie
Number of voters: 4
Vote: Alice
Vote: Bob
Vote: Charlie
Vote: Alice
Alice
```

**Background**

Elections come in all shapes and sizes. In the UK, the Prime Minister is
officially appointed by the monarch, who generally chooses the leader of the
political party that wins the most seats in the House of Commons. The United
States uses a multi-step Electoral College process where citizens vote on how
each state should allocate Electors who then elect the President.

Perhaps the simplest way to hold an election, though, is via a method commonly
known as the “plurality vote” (also known as “first-past-the-post” or “winner
take all”). In the plurality vote, every voter gets to vote for one candidate.
At the end of the election, whichever candidate has the greatest number of votes
is declared the winner of the election.

**Getting Started**

We are going to take the following code and complete the `vote` and
`print_winner` functions:

```c linenums="1"
#include <cs50.h>
#include <stdio.h>
#include <string.h>

// Max number of candidates
#define MAX 9

// Candidates have name and vote count
typedef struct
{
    string name;
    int votes;
}
candidate;

// Array of candidates
candidate candidates[MAX];

// Number of candidates
int candidate_count;

// Function prototypes
bool vote(string name);
void print_winner(void);

int main(int argc, string argv[])
{
    // Check for invalid usage
    if (argc < 2)
    {
        printf("Usage: plurality [candidate ...]\n");
        return 1;
    }

    // Populate array of candidates
    candidate_count = argc - 1;
    if (candidate_count > MAX)
    {
        printf("Maximum number of candidates is %i\n", MAX);
        return 2;
    }
    for (int i = 0; i < candidate_count; i++)
    {
        candidates[i].name = argv[i + 1];
        candidates[i].votes = 0;
    }

    int voter_count = get_int("Number of voters: ");

    // Loop over all voters
    for (int i = 0; i < voter_count; i++)
    {
        string name = get_string("Vote: ");

        // Check for invalid vote
        if (!vote(name))
        {
            printf("Invalid vote.\n");
        }
    }

    // Display winner of election
    print_winner();
}

// Update vote totals given a new vote
bool vote(string name)
{
    // TODO
    return false;
}

// Print the winner (or winners) of the election
void print_winner(void)
{
    // TODO
    return;
}
```

We can make up the following code for the `vote` and `print_winner` functions
that solves the problem:

```c linenums="1"
#include <cs50.h>
#include <stdio.h>
#include <string.h>

// Max number of candidates
#define MAX 9

// Candidates have name and vote count
typedef struct
{
    string name;
    int votes;
}
candidate;

// Array of candidates
candidate candidates[MAX];

// Number of candidates
int candidate_count;

// Function prototypes
bool vote(string name);
void print_winner(void);

int main(int argc, string argv[])
{
    // Check for invalid usage
    if (argc < 2)
    {
        printf("Usage: plurality [candidate ...]\n");
        return 1;
    }

    // Populate array of candidates
    candidate_count = argc - 1;
    if (candidate_count > MAX)
    {
        printf("Maximum number of candidates is %i\n", MAX);
        return 2;
    }
    for (int i = 0; i < candidate_count; i++)
    {
        candidates[i].name = argv[i + 1];
        candidates[i].votes = 0;
    }

    int voter_count = get_int("Number of voters: ");

    // Loop over all voters
    for (int i = 0; i < voter_count; i++)
    {
        string name = get_string("Vote: ");

        // Check for invalid vote
        if (!vote(name))
        {
            printf("Invalid vote.\n");
        }
    }

    // Display winner of election
    print_winner();
}

int get_index(string name)
{
    for (int i = 0; i < candidate_count; i++)
    {
        if (strcmp(name, candidates[i].name) == 0)
        return i;
    }
    return -1;
}

// Update vote totals given a new vote
bool vote(string name)
{
    int candidate_index = get_index(name); // gets the index for name user inputs
    if (candidate_index != -1)
    {
        candidates[candidate_index].votes++; // increments vote count for each candidate
        return true;
    }
    return false;
}

int get_max(void)
{
    int max_votes = candidates[0].votes;
    for (int i = 1; i < candidate_count; i++)
        if (candidates[i].votes > max_votes)
            max_votes = candidates[i].votes;

    return max_votes;
}

// Print the winner (or winners) of the election
void print_winner(void)
{
    int max_votes = get_max(); // see who has the most voites
    for (int i = 0; i < candidate_count; i++) // prints name of candidate with most votes
    {
        if (candidates[i].votes == max_votes)
            printf("%s\n", candidates[i].name);
    }
}
```

## Runoff

Now let's take the previous problem and make it a little more intricate.

You already know about plurality elections, which follow a very simple algorithm
for determining the winner of an election: every voter gets one vote, and the
candidate with the most votes wins.

But the plurality vote does have some disadvantages. What happens, for instance,
in an election with three candidates, and the ballots below are cast?

| Ballot | Ballot | Ballot | Ballot | Ballot  |
| ------ | ------ | ------ | ------ | ------- |
| Alice  | Alice  | Bob    | Bob    | Charlie |

A plurality vote would here declare a tie between Alice and Bob, since each has
two votes. But is that the right outcome?

There’s another kind of voting system known as a ranked-choice voting system. In
a ranked-choice system, voters can vote for more than one candidate. Instead of
just voting for their top choice, they can rank the candidates in order of
preference. The resulting ballots might therefore look like the below.

| Ballot    | Ballot    | Ballot    | Ballot    | Ballot    |
| --------- | --------- | --------- | --------- | --------- |
| 1.Alice   | 1.Alice   | 1.Bob     | 1.Bob     | 1.Charlie |
| 2.Bob     | 2.Charlie | 2.Alice   | 2.Alice   | 2.Alice   |
| 3.Charlie | 3.Bob     | 3.Charlie | 3.Charlie | 3.Bob     |

Here, each voter, in addition to specifying their first preference candidate,
has also indicated their second and third choices. And now, what was previously
a tied election could now have a winner. The race was originally tied between
Alice and Bob, so Charlie was out of the running. But the voter who chose
Charlie preferred Alice over Bob, so Alice could here be declared the winner.

One such ranked choice voting system is the instant runoff system. In an instant
runoff election, voters can rank as many candidates as they wish. If any
candidate has a majority (more than 50%) of the first preference votes, that
candidate is declared the winner of the election.

Let's look at the following code and see how we can implement this type of
voting system. We will need to fill in the correct code for the following
functions: `vote`, `tabulate`, `print_winner`, `find_min`, `is_tie`, and
`eliminate`.

```c linenums="1"
#include <cs50.h>
#include <stdio.h>

// Max voters and candidates
#define MAX_VOTERS 100
#define MAX_CANDIDATES 9

// preferences[i][j] is jth preference for voter i
int preferences[MAX_VOTERS][MAX_CANDIDATES];

// Candidates have name, vote count, eliminated status
typedef struct
{
    string name;
    int votes;
    bool eliminated;
}
candidate;

// Array of candidates
candidate candidates[MAX_CANDIDATES];

// Numbers of voters and candidates
int voter_count;
int candidate_count;

// Function prototypes
bool vote(int voter, int rank, string name);
void tabulate(void);
bool print_winner(void);
int find_min(void);
bool is_tie(int min);
void eliminate(int min);

int main(int argc, string argv[])
{
    // Check for invalid usage
    if (argc < 2)
    {
        printf("Usage: runoff [candidate ...]\n");
        return 1;
    }

    // Populate array of candidates
    candidate_count = argc - 1;
    if (candidate_count > MAX_CANDIDATES)
    {
        printf("Maximum number of candidates is %i\n", MAX_CANDIDATES);
        return 2;
    }
    for (int i = 0; i < candidate_count; i++)
    {
        candidates[i].name = argv[i + 1];
        candidates[i].votes = 0;
        candidates[i].eliminated = false;
    }

    voter_count = get_int("Number of voters: ");
    if (voter_count > MAX_VOTERS)
    {
        printf("Maximum number of voters is %i\n", MAX_VOTERS);
        return 3;
    }

    // Keep querying for votes
    for (int i = 0; i < voter_count; i++)
    {

        // Query for each rank
        for (int j = 0; j < candidate_count; j++)
        {
            string name = get_string("Rank %i: ", j + 1);

            // Record vote, unless it's invalid
            if (!vote(i, j, name))
            {
                printf("Invalid vote.\n");
                return 4;
            }
        }

        printf("\n");
    }

    // Keep holding runoffs until winner exists
    while (true)
    {
        // Calculate votes given remaining candidates
        tabulate();

        // Check if election has been won
        bool won = print_winner();
        if (won)
        {
            break;
        }

        // Eliminate last-place candidates
        int min = find_min();
        bool tie = is_tie(min);

        // If tie, everyone wins
        if (tie)
        {
            for (int i = 0; i < candidate_count; i++)
            {
                if (!candidates[i].eliminated)
                {
                    printf("%s\n", candidates[i].name);
                }
            }
            break;
        }

        // Eliminate anyone with minimum number of votes
        eliminate(min);

        // Reset vote counts back to zero
        for (int i = 0; i < candidate_count; i++)
        {
            candidates[i].votes = 0;
        }
    }
    return 0;
}

// Record preference if vote is valid
bool vote(int voter, int rank, string name)
{
    // TODO
    return false;
}

// Tabulate votes for non-eliminated candidates
void tabulate(void)
{
    // TODO
    return;
}

// Print the winner of the election, if there is one
bool print_winner(void)
{
    // TODO
    return false;
}

// Return the minimum number of votes any remaining candidate has
int find_min(void)
{
    // TODO
    return 0;
}

// Return true if the election is tied between all candidates, false otherwise
bool is_tie(int min)
{
    // TODO
    return false;
}

// Eliminate the candidate (or candidiates) in last place
void eliminate(int min)
{
    // TODO
    return;
}
```

Let's take a look at the `vote`, `tabulate`, `print_winner`, `find_min`,
`is_tie`, and `eliminate` functions to see what exactly we need to do.

**`vote`**

-   The function takes arguments `voter`, `rank`, and `name`. If `name` is a
    match for the name of a valid candidate, then you should update the global
    preferences array to indicate that the voter `voter` has that candidate as
    their `rank` preference (where `0` is the first preference, `1` is the
    second preference, etc.).

-   If the preference is successfully recorded, the function should return
    `true`; the function should return `false` otherwise (if, for instance,
    `name` is not the name of one of the candidates).

-   You may assume that no two candidates will have the same name.

**`tabulate`**

-   The function should update the number of `votes` each candidate has at this
    stage in the runoff.

-   Recall that at each stage in the runoff, every voter effectively votes for
    their top-preferred candidate who has not already been eliminated.

**`print_winner`**

-   If any candidate has more than half of the vote, their name should be
    printed to `stdout` and the function should return `true`.

-   If nobody has won the election yet, the function should return `false`.

**`find_min`**

-   The function should return the minimum vote total for any candidate who is
    still in the election.

**`is_tie`**

-   The function takes an argument `min`, which will be the minimum number of
    votes that anyone in the election currently has.

-   The function should return `true` if every candidate remaining in the
    election has the same number of votes, and should return `false` otherwise.

**`eliminate`**

-   The function takes an argument `min`, which will be the minimum number of
    votes that anyone in the election currently has.

-   The function should eliminate the candidate (or candidates) who have `min`
    number of votes.

Your program should behave per the example below:

```
./runoff Alice Bob Charlie
Number of voters: 5
Rank 1: Alice
Rank 2: Charlie
Rank 3: Bob

Rank 1: Alice
Rank 2: Charlie
Rank 3: Bob

Rank 1: Bob
Rank 2: Charlie
Rank 3: Alice

Rank 1: Bob
Rank 2: Charlie
Rank 3: Alice

Rank 1: Charlie
Rank 2: Alice
Rank 3: Bob

Alice
```

The correct code looks as follows:

```c linenums="1"
#include <cs50.h>
#include <stdio.h>
#include <string.h>

// Max voters and candidates
#define MAX_VOTERS 100
#define MAX_CANDIDATES 9

// preferences[i][j] is jth preference for voter i
int preferences[MAX_VOTERS][MAX_CANDIDATES];

// Candidates have name, vote count, eliminated status
typedef struct
{
    string name;
    int votes;
    bool eliminated;
}
candidate;

// Array of candidates
candidate candidates[MAX_CANDIDATES];

// Numbers of voters and candidates
int voter_count;  // global variable
int candidate_count; // global variable

// Function prototypes
bool vote(int voter, int rank, string name);
void tabulate(void);
bool print_winner(void);
int find_min(void);
bool is_tie(int min);
void eliminate(int min);

int main(int argc, string argv[])
{
    // Check for invalid usage
    if (argc < 2)
    {
        printf("Usage: runoff [candidate ...]\n");
        return 1;
    }

    // Populate array of candidates
    candidate_count = argc - 1;
    if (candidate_count > MAX_CANDIDATES)
    {
        printf("Maximum number of candidates is %i\n", MAX_CANDIDATES);
        return 2;
    }
    for (int i = 0; i < candidate_count; i++)
    {
        candidates[i].name = argv[i + 1];
        candidates[i].votes = 0;
        candidates[i].eliminated = false;
    }

    voter_count = get_int("Number of voters: ");
    if (voter_count > MAX_VOTERS)
    {
        printf("Maximum number of voters is %i\n", MAX_VOTERS);
        return 3;
    }

    // Keep querying for votes
    for (int i = 0; i < voter_count; i++)
    {

        // Query for each rank
        for (int j = 0; j < candidate_count; j++)
        {
            string name = get_string("Rank %i: ", j + 1);

            // Record vote, unless it's invalid
            if (!vote(i, j, name))
            {
                printf("Invalid vote.\n");
                return 4;
            }
        }

        printf("\n");
    }

    // Keep holding runoffs until winner exists
    while (true)
    {
        // Calculate votes given remaining candidates
        tabulate();

        // Check if election has been won
        bool won = print_winner();
        if (won)
        {
            break;
        }

        // Eliminate last-place candidates
        int min = find_min();
        bool tie = is_tie(min);

        // If tie, everyone wins
        if (tie)
        {
            for (int i = 0; i < candidate_count; i++)
            {
                if (!candidates[i].eliminated)
                {
                    printf("%s\n", candidates[i].name);
                }
            }
            break;
        }

        // Eliminate anyone with minimum number of votes
        eliminate(min);

        // Reset vote counts back to zero
        for (int i = 0; i < candidate_count; i++)
        {
            candidates[i].votes = 0;
        }
    }
    return 0;
}

// Record preference if vote is valid
bool vote(int voter, int rank, string name)
{
    // TODO
    for (int i = 0; i < candidate_count; i++)
    {
        if (strcmp(candidates[i].name, name) == 0)
        {
            preferences[voter][rank] = i;
            return true;
        }
    }
    return false;
}

// Tabulate votes for non-eliminated candidates
void tabulate(void)
{
    // TODO
    for (int i = 0; i < voter_count; i++)
    {
        for (int j = 0; j < candidate_count; j++) // j is rank
        {
            int candidate_index = preferences[i][j];
            if (!candidates[candidate_index].eliminated)
            {
                candidates[candidate_index].votes++; // update vote count if candidate has not been eliminated
                break;
            }
        }
    }
}

// Print the winner of the election, if there is one
bool print_winner(void)
{
    // TODO
    for (int i = 0; i < candidate_count; i++)
    {
        if (candidates[i].votes > (voter_count / 2)) // checks to see if one candidate has over half the votes
        {
            printf("%s\n", candidates[i].name);
            return true;
        }
    }
    return false;
}

// Return the minimum number of votes any remaining candidate has
int find_min(void)
{
    // TODO
    int min = 0; // start from zero
    bool find_first = false;
    for (int i = 0; i < candidate_count; i++)
    {
        if (!candidates[i].eliminated) // see if candidate has been eliminated
        {
            if (!find_first)
            {
                min = candidates[i].votes;
                find_first = true;
            }
            else if (candidates[i].votes < min)
            {
                min = candidates[i].votes;
            }
        }
    }
    return min;
}

// Return true if the election is tied between all candidates, false otherwise
bool is_tie(int min)
{
    // TODO
    for (int i = 0; i < candidate_count; i++)
    {
        if (!candidates[i].eliminated)
            if (candidates[i].votes != min)
                return false;
    }
    return true;
}

// Eliminate the candidate (or candidiates) in last place
void eliminate(int min)
{
    // TODO
    for (int i = 0; i < candidate_count; i++)
    {
        if (!candidates[i].eliminated)
        {
            if (candidates[i].votes == min)
                candidates[i].eliminated = true;
        }
    }
}
```
