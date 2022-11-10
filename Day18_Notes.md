# Day 18: Tips on Building a Program from Scratch
#### CS65: Introduction to Computer Science 1

Wednesday, November 9th, 2022

[⏮ Go back to Day17](https://github.com/merriekay/CS65-Notes/blob/main/Day17_Make_a_Game.ipynb) 

## Admin Stuff:
- __Lab #13__ due Thursday, November 10th by 6:00 pm. __Make a Dice Game__, see [Day17](https://github.com/merriekay/CS65-Notes/blob/main/Day17_Make_a_Game.ipynb) for more details.
    - To be judged by my game night friends, winner will get either something silly from the dollar store or a chance to 3D print something


## Quick Review:

Last class we talked about:
- `roll_die()` function
- rolling multiple dice


# Building From Scratch:
In class on Monday, I noticed that we haven't done a lot of creating your own program from scratch, and I wanted to take some time today to really dig in to what that process looks like, and demonstrate some best practices for this.

## Here are some tips: 

### Step #1: Start by planning/writing out __what you want your software to do__. 
- For this assignment, it might look something like playing a few games and deciding how you want your game to operate. 

## Step #2: __break the project down into smaller units__.

- For a dice game, this might look like building pieces like `roll_die`, `roll_multiple_dice`, `get_score`, `user_interaction`, maybe printing out the results of a roll, etc... These will probably become functions in your program.

- Now, __break those units down even further__. 
    - __Docstrings__ are great here: Can you define what the input and outputs (parameters/returns) should be for each of these functions? Maybe start writing a quick description of what the function should do?


## Step #3: Write your first line of code, and inevitably, get stuck.
- Getting stuck is always going to be part of coding. The sooner you make peace with that the sooner you can stop beating yourself up or feeling like an imposter. 
- The best coders are not the ones who get the program right the first time, they're the ones who develop a strong since of __resiliency and an ability to push through the frustration of being stuck__. 

### Tips on Getting Unstuck:
- Google is your friend
- taking a break and doing something else helps a lot. 
- Ask a friend, or even just explain what you're doing to someone else (even if they've never written a line of code). 
    - This is called the 🐥 _rubber ducky_ debugging method--explaining your code to a rubber ducky. 
    
- __Test your code early and often__: You should never write more than 5-10 lines of code without testing that it works how you expect. 
    - `print()` statments are you friend here, but we generally don't want them to stick around. Once you've verified that your function works how you want it to, feel free to delete the print statements.

## Step #4: Start simple and build to be more complicated. 
- It can be tempting to jump right in and try to implement the entire project in one go, but this often leads to frustration. 
- __✨Perfection is not the goal__--even Google is not perfect. Making small incremental improvements is a much better philosophy when it comes to building out a software project.
- It generally works better to start by implmenting a small piece of code, test it, and then more on to the next one. Slowly, you can build to a more complex end-product.
> Does your game have 10 different scoring rules? That's great, but you should start by building out one rule, and then testing it. Then build the next one, and... you guessed it... Test it.

# Back to the Dice Game Project:

Let me demonstrate some of these concepts by working through building a dice game of my own.

Everyone started with the `roll_die()` function:


```python
import random

def roll_die(num_sides):
    """
    Will return a random number between 1 and num_sides, as a dice would.
    
    Parameters:
        num_sides: the upper bound on the random number
    Return:
        a random number between 1 and num_sides, inclusive.
    """
    return random.randint(1,num_sides)
print(roll_die(6))
```

    1


Then, in class yesterday, I showed you some code that can relatively easily be built into the `roll_multiple_dice` function:


```python
def roll_multiple_dice(num_dice, num_sides):
    """
    Will return a list with num_dice elements which are random numbers between 1 and num_sides
    
    Parameters:
        num_dice: the number of dice to roll
        num_sides: the number of sides the dice should have (must all have the same number of sides)
    Return:
        roll, the list of random numbers rolled
    """
    roll = []
    for x in range(num_dice):
        roll.append(roll_die(num_sides))
    return roll
print(roll_multiple_dice(4, 6))
```

    [2, 6, 3, 5]


A common part of scoring dice games it to be able to know things like: 
- "How many ones were in the roll?"
- "How many sixes were in the roll?"
- etc...

## Group Exercise: 
So let's build a `how_many()` function.


```python
def how_many(val, roll):
    """
    returns the number elements in the roll list that have the value of val
    
    Parameters:
        val, the number/value to check for
        roll, a given dice roll to check
    Return:
        the number of times a roll has the value num.
    """
    counter = 0
    for x in roll:
        if x == val:
            counter +=1
    return counter
    
print(how_many(6, [1,4,6,4]))
```

    1


Another way of doing this uses the `.count()` list method:
>But... you might need to include a for loop, so the function above might be a better call.


```python
my_list = [1,4,5,1,6]
print(my_list.count(6))
```

    1



```python
#Let's pull things together a bit:
num_of_sides = 6
num_of_dice = 4

p1_roll = roll_multiple_dice(num_of_dice,num_of_sides) #roll 4, 6-sided dice
p2_roll = roll_multiple_dice(num_of_dice,num_of_sides)

#check to see how many 1s in each roll
#p1_ones = how_many(1, p1_roll)
#p2_ones = how_many(1, p2_roll)
#or
p1_ones = p1_roll.count(1)
p2_ones = p1_roll.count(1)

print(p1_roll)
for x in range(1, num_of_sides + 1):
    #print("P1 roll has ", how_many(x, p1_roll),' ', x,'s', sep='')
    print("P1 roll has ", p1_roll.count(x), ' ', x,'s', sep='')

```

    [6, 5, 6, 2]
    P1 roll has 0 1s
    P1 roll has 1 2s
    P1 roll has 0 3s
    P1 roll has 0 4s
    P1 roll has 1 5s
    P1 roll has 2 6s


## 💾 🎲 Saving and Re-Rolling Dice 
A lot of dice games rely on the idea of 'saving' specific dice from a roll and re-rolling the rest.

Let's start by writing out some __pseudocode__ of how we might accomplish this.


```python
# Pseudo code:
"""
Step 1: start with a roll of multiple dice
Step 2: User interaction--which dice would you like to save?
Step 3: Get the dice that the user wants and put them in a new list
Step 4: Update the number of dice to roll
"""
```

## Reminder: `split()` function

Remember this guy? `split()` is a super helpful string function that takes in a string, and returns a list where the elements are part of the input string split into pieces.


```python
'   1  2   3     4 5'.split()
```




    ['1', '2', '3', '4', '5']




```python
'how does this function work?'.split()
```




    ['how', 'does', 'this', 'function', 'work?']




```python
'1,2,3,4,5,6'.split(',')
```




    ['1', '2', '3', '4', '5', '6']



Using the `split()` function, we can take a user's input (initially a string), and convert it into a list of integers like so: 


```python
user_input = input("enter a list of numbers:")

user_list = user_input.split(',')
int_list = [(int(num)) for num in user_list]
print(int_list)
```

    enter a list of numbers:6,7
    [6, 7]


Now, we can pull together some of the parts that we've already built to implement our pseudocode.

Questions to consider: 
- how might you split this code into functions?
- can you make it so the code below loops until there are no dice left to roll?


```python
# get the initial roll
num_of_sides = 6
num_of_dice = 4
p1_roll = roll_multiple_dice(num_of_dice,num_of_sides) #roll 4, 6-sided dice
print(p1_roll)

#get the user input and convert it to a list of integers
dice_to_save = input("which dice would you like to save? (enter the position numbers separated by a comma) ")
user_list = dice_to_save.split(",")
int_list = [(int(num)) for num in user_list]

#create a new empty list to save specific dice
save_list = []

#use a for loop to save the dice at the indices entered by the user
for x in int_list:
    save_list.append(p1_roll[x-1]) #why is it x-1 rather than x?
print("you saved:", save_list)
```

    [5, 3, 2, 6]
    which dice would you like to save? (enter the position numbers separated by a comma) 1,2
    you saved: [5, 3]



```python
def user_interaction(roll, save_list):
    """
    Get the values to save from the user and return a list of the saved dice
    
    Parameters:
        roll, the roll that we're working with
        save_list, the list of dice that are 'saved'
    Return:
        the list of dice that the user chose to save.
    """
    dice_to_save = input("Which dice would you like to save? ")
    user_list = dice_to_save.split(",")
    int_list = [(int(num)) for num in user_list]
    for x in int_list:
        if x !=0:
            save_list.append(roll[x-1])
    print()
    print("You saved:", save_list)
    
    return save_list

saved = user_interaction([1,1,3,4],[])
print(saved)
```

    Which dice would you like to save? 1,2
    
    You saved: [1, 1]
    [1, 1]


## All together it might look something like this:

I split the code on the previous slide into the following functions:
- `user_interaction`: Get the values to save from the user and return a list of the saved dice
- `game_loop`: runs the main game loop using all of the other functions

I also added a couple helper funtions: 
- `get_score`: which will take in a roll and determine the score (right now it is pretty simple, but has room to be made more complext)
- `print_instructions`: will output some text to the console for the user to understand how to interact with the game.

Let's copy this code over to Thonny and take a closer look: 


```python
import random

def roll_die(num_sides):
    """
    Will return a random number between 1 and num_sides, as a dice would.
    
    Parameters:
        num_sides: the upper bound on the random number
    Return:
        a random number between 1 and num_sides, inclusive.
    """
    return random.randint(1,num_sides)

def roll_multiple_dice(num_dice, num_sides):
    """
    Will return a list with num_dice elements which are random numbers between 1 and num_sides
    
    Parameters:
        num_dice: the number of dice to roll
        num_sides: the number of sides the dice should have (must all have the same number of sides)
    Return:
        roll, the list of random numbers rolled
    """
    roll = []
    for x in range(num_dice):
        roll.append(roll_die(num_sides))
    return roll

def how_many(val, roll):
    """
    returns the number elements in the roll list that have the value of num
    
    Parameters:
        val, the number/value to check for
        roll, a given dice roll to check
    Return:
        the number of times a roll has the value num.
    """
    counter = 0
    for die in roll:
        if die == val:
            counter += 1
    return counter

def user_interaction(roll, save_list):
    """
    Get the values to save from the user and return a list of the saved dice
    
    Parameters:
        roll, the roll that we're working with
        save_list, the list of dice that are 'saved'
    Return:
        the list of dice that the user chose to save.
    """
    dice_to_save = input("Which dice would you like to save? ")
    user_list = dice_to_save.split(",")
    int_list = [(int(num)) for num in user_list]
    for x in int_list:
        if x !=0:
            save_list.append(roll[x-1])
    print()
    print("You saved:", save_list)
    
    return save_list

def get_score(dice_list):
    #insert code here to calculate the score
    #the how_many() function might come in handy here
    score = how_many(1,dice_list) *100
    score += how_many(2,dice_list) *200
    #etc
    
    return score

def print_instructions():
    print("To 'save' a die, enter the position it is in the roll, for example, if your roll was [4,3,5,2], and you wanted to save the 3 and 2, you would type 2, 4.")
    print("If you do not want to save any dice, enter 0.")

def game_loop():
    #set your variables
    num_of_sides = 6
    dice_to_roll = 4
    saved = []
    
    print_instructions()
    print("=========================")
    while dice_to_roll > 0 :
        #get the roll
        p1_roll = roll_multiple_dice(dice_to_roll,num_of_sides)
        print()
        print("Your roll:", p1_roll)

        #ask the user which dice they want to save
        old_saved_len = len(saved)
        saved = user_interaction(p1_roll, saved)
        new_saved_len = len(saved)
        
        dice_saved_this_round = new_saved_len - old_saved_len
        if dice_saved_this_round > 0:
            dice_to_roll = dice_to_roll - len(saved)
    print()
    print("You scored:", get_score(saved))

game_loop()
```

    To 'save' a die, enter the position it is in the roll, for example, if your roll was [4,3,5,2], and you wanted to save the 3 and 2, you would type 2, 4.
    If you do not want to save any dice, enter 0.
    =========================
    
    Your roll: [2, 2, 3, 2]
    Which dice would you like to save? 1,2,4
    
    You saved: [2, 2, 2]
    
    Your roll: [2]
    Which dice would you like to save? 1
    
    You saved: [2, 2, 2, 2]
    
    You scored: 800


## Admin Stuff:
- __Lab #13__ due Thursday, November 10th by 6:00 pm. __Make a Dice Game__, see [Day17](https://github.com/merriekay/CS65-Notes/blob/main/Day17_Make_a_Game.ipynb) for more details.
    - To be judged by my game night friends, winner will get either something silly from the dollar store or a chance to 3D print something

