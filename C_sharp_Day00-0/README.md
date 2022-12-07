# Day 00 – .NET Boot camp
### Procedural C#

# Contents
1. [Chapter I](#chapter-i) \
	[General Rules](#general-rules)
2. [Chapter II](#chapter-ii) \
	[Rules of the Day](#rules-of-the-day)
3. [Chapter III](#chapter-iii) \
	[Exercise 00 – Life on credit](#exercise-00-life-on-credit)
4. [Chapter IV](#chapter-iv) \
	[Exercise 01 – Working out the bugs](#exercise-01-working-out-the-bugs)


# Chapter I 

## General Rules
- Make sure you have [the .NET 5 SDK](<https://dotnet.microsoft.com/download>) installed on your computer and use it.
- Remember, your code will be read! Pay special attention to the design of your code and the naming of variables. Adhere to commonly accepted [C# Coding Conventions](<https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions>).
- Choose your own IDE that is convenient for you.
- The program must be able to run from the dotnet command line.
- Each of the tasks contains the input parameters and the format of the output response. You must adhere to them. 
- At the beginning of each task, there is a list of allowed language constructs.
- If you find the problem difficult to solve, ask questions to other piscine participants, the Internet, Google or go to StackOverflow.
- You may see the main features of C# language in [official specification](<https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/introduction>). 
- You demonstrate the complete solution, the correct result of the program is just one of the ways to check its correct operation. Therefore, when it is necessary to obtain a certain output as a result of the work of your programs, it is forbidden to show a pre-calculated result.
- Pay special attention to the terms highlighted in **bold** font: their study will be useful to you both in performing the current task, and in your future career of a .NET developer.
- Have fun :)


# Chapter II
##  Rules of the Day
- All projects must be in the same solution.
- Each of the tasks must correspond to a separate console application created based on a standard .NET SDK template.
- Use **top-level-statements**  and **var**.
- The name of the project (and its separate catalog) should look like d{xx}_ex{yy}, where xx is the digits of the current day, yy is the digits of the current task.
- The name of the solution (and its separate catalog) is d_{xx}, where xx are the digits of the current day.
- To format the output data, use the en-GB **culture**: N2 for the output of monetary amounts, d for dates.
- In mathematical calculations, use rounding up to hundredths.

Since in the first lesson we consider the language as a procedural one:
- You can't use classes. Yes, the Program class too!
- You cannot use nuget packages.


# Chapter III
## Exercise 00 – Life on credit

“As my father used to say: "There are two sure ways to lose a friend, one is to borrow, the other to lend.”

**― Patrick Rothfuss, The Name of the Wind**

### Allowed language constructs

- Local functions
- Loops
- If/else statements
- Casting and type conversion
- DateTime and its methods
- System.Math and its methods
- CultureInfo


### Project structure:
```
d00_ex00
  Program.cs

```

### The objective

In order to study at School 21 and not be left without a living, you decided to take out a loan. Or, at least, you consider the option of such a development of events. Well, you think, having decided to calculate everything in advance, why not make a schedule of upcoming payments?

Let it look like a table of the following type: 

| Payment no. | Payment date | Payment | Principal debt | Interest | Remaining debt  |
|---|---|---|---|---|---|
 
Everything will be calculated monthly. And for these calculations, it is enough that your calculator accepts at the input: The loan amount, the Annual percentage rate, the number of months of the loan.
 
You open the loan agreement and see the formulas that the bank uses to make calculations:

**Total monthly payment**

```math

\frac{Loan \; ammount*i*(1+i)^n}{(1+i)^n-1}

```

n — number of months, when the loan is paid

i — the interest rate on the loan per month.

**Interest rate on the loan per month:**

```math

i = Annual \; percentage \; rate /12/100

```

**Monthly payment interest:**

```math

\frac{Total \; debt \; balance*Annual \; percentage \; rate * DaysOfThePeriod}{100*Days \; per \; year}

```

The total debt balance is the amount of the principal debt as of the settlement date.

The number of days of the period is the difference in days between the "Current payment date" and the date of the previous payment.

It seems complicated, but let’s figure it out. 

We assume that you pay off the loan on the 1st day of each month, starting from the next. It's important to consider leap years! The **System.DateTime**  methods will help you with this and other operations with dates and times. In total, there will be as many such months as you took out the loan for (the input argument).

The monthly payment (_Payment_) consists of the part going to the repayment of the principal debt (_Principal debt_), and the part going to the payment of interest on the loan (_Interest_). The formulas for calculating the Amount of the monthly payment (_Payment_) and the Interest of the monthly payment (_Interest_) are given in the loan agreement above. For mathematical calculations, use the tools of the **System.Math** library. Now, knowing them, you can calculate the _Principal Debt_.

The _Remaining debt_ for each month is also easy to determine: we simply gradually subtract the monthly payment from the total loan amount. **Loops** and **increment operators** will help you here. Note that if this is the last month of the loan and the balance of the debt is non-zero, you just need to increase the monthly payment and the amount going to pay the debt in the schedule. So we’ll pay the loan off in time.

The last step is to bring everything into a nice and convenient table. **Linear interpolation** and **tabs and string break characters** will help you. 

Loans have never been so much fun! Have they?..

### Input parameters

Don't forget about [converting strings to numbers](<https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/types/how-to-convert-a-string-to-a-number>)!

| Argument | Type | Description |
|---|---|---|
| sum |double | Loan amount, RUB |
|rate | double | Annual percentage rate, % |
|term|int|Number of months of the loan|

### Output format

The data should be ordered by month (in ascending order).

#### The user specified incorrect data
```
Something went wrong. Check your input and retry.
```
#### Examples of launching an application from the project folder
```
$ dotnet run 1000000 12 10
1       06/01/2021      105,582.08      95,390.30       10,191.78       904,609.70
2       07/01/2021      105,582.08      96,659.90       8,922.18        807,949.81
3       08/01/2021      105,582.08      97,347.63       8,234.45        710,602.18
4       09/01/2021      105,582.08      98,339.77       7,242.30        612,262.40
5       10/01/2021      105,582.08      99,543.32       6,038.75        512,719.08
6       11/01/2021      105,582.08      100,356.56      5,225.52        412,362.52
7       12/01/2021      105,582.08      101,514.94      4,067.14        310,847.58
8       01/01/2022      105,582.08      102,413.99      3,168.09        208,433.60
9       02/01/2022      105,582.08      103,457.77      2,124.31        104,975.83
10      03/01/2022      105,942.18      104,975.83      966.35          0.00
```
```
$ dotnet run 55000 10 20
1       06/01/2021      2,996.95        2,529.82        467.12        52,470.18
2       07/01/2021      2,996.95        2,565.68        431.26        49,904.49
3       08/01/2021      2,996.95        2,573.10        423.85        47,331.39
4       09/01/2021      2,996.95        2,594.95        401.99        44,736.44
5       10/01/2021      2,996.95        2,629.25        367.70        42,107.19
6       11/01/2021      2,996.95        2,639.32        357.62        39,467.87
7       12/01/2021      2,996.95        2,672.55        324.39        36,795.32
8       01/01/2022      2,996.95        2,684.44        312.51        34,110.88
9       02/01/2022      2,996.95        2,707.24        289.71        31,403.64
10      03/01/2022      2,996.95        2,756.04        240.90        28,647.60
11      04/01/2022      2,996.95        2,753.64        243.31        25,893.97
12      05/01/2022      2,996.95        2,784.12        212.83        23,109.85
13      06/01/2022      2,996.95        2,800.67        196.28        20,309.18
14      07/01/2022      2,996.95        2,830.02        166.92        17,479.16
15      08/01/2022      2,996.95        2,848.49        148.45        14,630.66
16      09/01/2022      2,996.95        2,872.69        124.26        11,757.98
17      10/01/2022      2,996.95        2,900.30        96.64         8,857.67
18      11/01/2022      2,996.95        2,921.72        75.23         5,935.96
19      12/01/2022      2,996.95        2,948.16        48.79         2,987.80
20      01/01/2023      3,013.18        2,987.80        25.38         0.00
```
# Chapter IV
## Exercise 01 – Working out the bugs

“Never interrupt your enemy when he is making a mistake.”

**― Napoleon Bonaparte**

### Allowed language constructs

- Local functions
- Loops
- If/else statements
- string and its methods
- System.IO

### Project structure:
```
d00_ex01
  Program.cs
```

### The objective

Credit or no credit, let's imagine that you found a good job with a schedule that will allow you to study comfortably at School 21, and even sharpen the skills you learned at school. And here in a new place the first task comes to you: «Implement auto-correction of the user name».

The fact is that users are not always attentive to filling out forms and make typos. But there is a dictionary that contains a list of all the names, by which you can check the correctness of the spelling, and in response to an error in the user name it can offer a correction. This is what you need to implement.

You have a file with a list of all English-language names attached to the lesson. You need to read a list of names for verification from it. Don't copy the text to code! There are more convenient ways, look towards **File.IO**. 

Here we assume the dictionary is complete and contains all possible options (if the user selects nothing or the name is not found, an error is displayed).

You decide to use [Levenshtein distance](<https://en.wikipedia.org/wiki/Levenshtein_distance>) to compare words. We consider the name related to the entered one if the editing distance to it is less than 2. Choose for yourself whether to use loops or recursion. The easiest way to perform operations with strings, such as clearing them from extra spaces, is to use methods of the **string** type.

So, you need to implement a console application that asks for a username:

```
>Enter name:
```

### Output format

Next, the user must enter their name (it can contain only letters, spaces and hyphens), to which the program reacts in the following way.

| Case | Expected output |
|---|---|
| Name was found in the dictionary |Hello, {name}! |
| A close name was found in the dictionary (the editing distance to which is no more than 1) |>Did you mean “{corrected name}”? Y/N |
| Y |Hello, {corrected name}! |
| N |>Did you mean “{new correction option}”? Y/N <br/> or <br/> Your name was not found. |
| No related name was found |Your name was not found. |
| Name not entered  |Your name was not found. |

#### The user specified incorrect data
```
Something went wrong. Check your input and retry.
```

#### Examples of launching an application from the project folder

```
$ dotnet run
>Enter name:
Mrk
>Did you mean “Mark”? Y/N
Y
>Hello, Mark!
```
