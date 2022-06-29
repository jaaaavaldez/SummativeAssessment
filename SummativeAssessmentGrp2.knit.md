---
title: "SUMMATIVE ASSESSMENT"
author:
- Tina Almario, Aze Peñalosa, Manu Perez, 
- Justin Tan, Ja Valdez, Jaime Villarosa
date: '2022-06-27'
output:
  html_document: 
    self_contained: yes
---

<style>

h1.title {
  font-style: bold;
  text-align: center;
  color: #D792B9;

}

h4.author, h4.date, h4 {
  text-align: center;

}

h3 {
  text-align: center;
  color: #2F3337;

}

body {
  font-size: 14pt;
  text-align: justify;
}

.outline {
  border-radius: 25px;
  border: 2px solid #2F3337;
  padding: 20px; 
  width: auto;
  height: auto;  
}

</style>

---

### **SAY HELLO TO RMO!**

![](https://live.staticflickr.com/65535/52178902506_936f7d9a86_h.jpg)

> RMO is right! For this *Summative Assessment*, we will explore the following problems: the **Monty Hall Problem** and the **Ultra Lotto Problem**. 

![](https://live.staticflickr.com/65535/52178882473_623c7932a6_c.jpg) 

### <b>GENERAL GIST OF THE PROBLEM</b>  

Monty Hall was a game show host and the person this popular problem originates and is named from. The contestant would have **3 doors to choose from**, behind one of them was a car. The problem comes in when Monty opens one of the other 2 doors. Monty, knowing which door has the car, would then obviously open the door without a car. You are then left with the decision of whether to **keep your original answer**, or to **switch to the other remaining door**. Only years later would people realize that there is in fact a decision you should always make.

![](https://live.staticflickr.com/65535/52179570508_4b604d3c13_k.jpg)


<p class="outline">The **Monty Hall Problem** will be discussed following the outline: <br><br>
1. *Why Switch and Why Not* <br> 
2. *Using Concepts of Probability* <br> 
3. *Program Simulation Using Python* <br>
</p>

### <b>WHY SWITCH AND WHY NOT</b>  

> The main argument for not switching in this scenario is that since there are only two options left, the probability of getting the right answer would only be a 50-50. This would mean that there would be no benefit to switching. Due to this, the participants would tend to trust their initial answer. Aside from this, there is not really any other particular reason not to switch.  

> The reason why switching is the answer you should always take can be more easily grasped when viewing the situation as a whole. In the beginning, the door you chose is one of three options, meaning that there is a one-third chance of choosing the right door. It is through this initial probability where we arrive at the conclusion that **switching is always the best option**. As the door you initially chose has a one-third chance of being correct, there is a two-thirds chance of the car being in one of the other two doors. Because one of those doors were already opened, this consolidates that two-thirds chance onto the other door as the game show host would obviously not open the door with the car.


### <b>USING CONCEPTS OF PROBABILITY</b>
> To further visualize the approach to this situation, we aim to present solutions to the Monty hall problem using concepts of Probability. In the standard problem, there are three doors, and as such there is a sample space of three possible outcomes for the arrangement of the goats and car. These can be listed as (C, G, G), (G, C, G), (G, G, C). When the contestant takes their first pick for a door, there is only one outcome that gives them the car on that pick. As the complement to that however, there are two other outcomes that give a goat on their first pick. As such, the probability of the first chosen door being a goat is 2/3, and that of the first chosen door being a car is 1/3. When the host opens one of the other doors, it is sure to be a goat. After one of the doors is eliminated through this, and because of the initial probabilities established previously, the probability of a car being behind the remaining door is 2/3, and that of a goat is 1/3.
>
>For example, let us refer back to the three possible outcomes, and assume that the contestant picked door one. The only way they can win the car with this choice is from outcome one, but there are two other outcomes where they picked a goat, making that more likely with a probability of 2/3. When another door is opened by the host, it eliminates that door, as it already has a goat. When looking back at the outcomes, you can eliminate one G door (as long as it is not also door one, as that is what the contestant picked). It is now apparent that in both outcome two and three, the remaining door will contain the car, whereas only in outcome one will the initially chosen door one have the car. This makes it clear that switching is the best choice.
>
>A modified version of the Monty Hall Problem was created by researchers Chen and Wang to help people better understand the circumstances of the paradox in regards to probability (Chen & Wang, 2020). They made a version of the game with 100 doors instead of 3; with 99 goats and 1 car, after the contestant’s initial choice, the hosts revealed 98 doors with goats in them, subsequently asking the contestant whether they would like to switch or stay.
>
![](https://static.wikia.nocookie.net/game-theory/images/6/6a/Monty_Hall%2C_Plinko%2C_and_Probability.jpg/revision/latest/scale-to-width-down/1000?cb=20160809222109) 
>
>The researchers were able to create equations to visualize the situations in the 100 door version. In our case, let variable K be the number of doors; one will have a car behind it, and the other K-1 will have a goat. After the initial choice, K-2 doors will be opened to reveal goats, and the host can choose to switch or stay. It was determined that the probability of winning a car is (K-1)/K, and with an example of K=100 doors, this probability will be 99/100. Translating this back to a 3-door situation, the probability will be (3-1)/3 = 2/3. The study was also able to show that presenting the 100–door version made contestants more willing to switch doors in the 3-door version, thus giving them a higher chance of winning.


### <b>MONTY HALL SIMULATION USING R</b> {.tabset .tabset-fade .tabset-pills}

#### About the Simulation

> The discussed mathematical theorem implies that always switching after one door is opened serves as the most sensible choice. We can push the concept of the Monty Hall problem by exploring it through an **original simulation based on R program**. Right before knitting the HTML, the program ran through one hundred thousands test runs.
>
> Explore the program by navigating through the tabs, where the rate of success given three doors with one car and two goats that are randomly arranged is shown at the bottom of the R program.

#### Simulation 1: Never Switching

> The code is shown below. Comments are readily available to guide readers through the program.


```r
winCtr <- 0
trials <- 100000

#this program simulation executed 100 thousand test runs to get the approximate value of the probability of winning
for(total in 0:trials){
  
  #real list signifies the actual positions of the two goats and one car
  real <- c(0,0,0)
  #pick list represents the initial guess of the player
  pick <- c(0,0,0)
  sum <- c(0,0,0)
  
  #generate the actual order and the guessed order
  real[sample(1:3,1)] = 1
  pick[sample(1:3,1)] = 1
  
  #add the corresponding elements of the two vectors
  sum <- c(real[1]+pick[1], real[2]+pick[2], real[3]+pick[3])
  
  
  if(2 %in% sum){
    #the presence of '2' in the sum vector means that the player's guess coincides with the reality
    winCtr <- winCtr + 1
    #program simulation counts this as one win
  }
}

#program simulation displays the probability of winning after finishing the 100 thousand test runs
cat("Success Rate: ", (winCtr/total)*100, "%")
```

```
## Success Rate:  33.29 %
```

> <b>Let's Discuss:</b>
> Setting the simulation to never switch even after the host opens one door yields a success rate that approaches 33%, which coheres with the mathematical theorem discussed. Staying with the initial guess corresponds to the simple probability of getting that one car out of three doors, which is exactly 1/3.

#### Simulation 2: Always Switching

> The code is shown below. Comments are readily available to guide readers through the program.


```r
#TEST 1: ALWAYS CHANGING DOORS 

winCtr <- 0
trials <- 100000

#this program simulation executed 100 thousand test runs to get the approximate value of the probability of winning
for (total in 0:trials){
  
  #basic initializations
  open <- 0
  lastPick <- 0
  
  #three doors exists: '0' denotes the goat while '1' represents the car
  #note only one car hides behind the three doors
  
  #real vector signifies the actual positions of the two goats and one car
  real <- c(0,0,0)
  #pick vector represents the initial guess of the player
  pick <- c(0,0,0)
  
   #loc vector notes down the location/index of the doors that the player did not choose
  loc <- c(1,2,3)
  
  sum <- c(0,0,0)
  
  
  #generate the actual order and the guessed order
  real[sample(1:3,1)] = 1
  pick[sample(1:3,1)] = 1
  
  #add the corresponding elements of the two vectors
  sum <- c(real[1]+pick[1], real[2]+pick[2], real[3]+pick[3])
  
  if(2 %in% sum){
    
    #the presence of '2' in sum implies that the player guessed right initially
    loc <- loc[-(which(sum == 2))]
    
    #the host opens a random door that has a goat and the player hasn't guessed
    open <- loc[sample(1:2,1)]
    
    #the simulation then deletes the opened door out of the lists
    real <- real[-open]
    pick <- pick[-open]
    sum <- sum[-open]
    
    #only two choices now remain
    #the following the Monty Hall concept, the player changes door
    #changing from '2' to '0' in the sum list
    
    lastPick <- loc[which(sum == 0)]
    
    if(lastPick == 2){
      #simulation will never flow through here
      winCtr = winCtr + 1
    }
    #the player would never get the car in this condition
    
  } else{
    #the absence of '2' implies that the player's guess was initially wrong
    
    #the host opens that ONE door that has a goat and the player hasn't guessed
    open <- which(sum == 0)
    
     #the simulation then deletes the opened door out of the vectors
    real <- real[-open]
    pick <- pick[-open]
    sum <- sum[-open]
    
    #only two choices now remain
    #the following the Monty Hall concept, the player changes door
    #the door where the player changes to is already certain (to the index with a '0' element in the pick list)
    
    lastPick <- which(pick == 0)
    pick = c(0,0)
    pick[lastPick] <- 1
    
     #the sum of the two lists containing two elements is summed up
    sum <- c(real[1]+pick[1], real[2]+pick[2])

    if(2 %in% sum){
      #an element of '2' corresponds to a correct guess and the simulation counts that as one win
      #program simulation always flows to this condition if the player's guess was initially wrong
      winCtr = winCtr + 1
    }
  }
}

cat("Success Rate: ", (winCtr/total)*100, "%")
```

```
## Success Rate:  66.327 %
```

<b>*Let's Discuss:*</b> <br>

> This simulation confirmed the mathematical principle that **switching leads to a higher success rate of around 66%**. Largely deducing from the flow of the program shows, it follows that two major conditions exists:
> 1. The player initially chooses right.
> 2. The player initially chooses wrong.
> Switching choices for the first condition will certainly lead to a wrong choice while likewise changing choices for the second condition always leads to the right choice. Since only two doors remain after the host revealed one door containing the goat, the unselected door must have the car given that the initial guess is wrong.
>
> Notice that a reversal occurs, in which right choice becomes wrong and vice versa. Thus, the success rate of changing the choice after one door opens corresponds to the complement of the probability of the alternative: 1/3. It follows that its complement is 2/3, which is approximately 66%.




### ---

![](https://live.staticflickr.com/65535/52179365205_0dea884dfd_c.jpg) 

![*\*see calculations below*](https://live.staticflickr.com/65535/52180617865_86593dba87_k.jpg) 

### <b>ULTRA LOTTO PROBLEM: MATHEMATICAL SOLUTION</b>

In lotteries, the order of selection of the numbers *do not matter*. Hence, solving for the number of all possible combinations in the Ultra Lotto 6/58 employs **Combinations** since they consider any un-ordered arrangement of objects from a collection. 

*Note* that the **Combination Formula** is given as:

$$
_{n}C_{r} = \frac{n!}{r!(n-r)!}
$$

where $r$ is the number of objects that can be formed from a collection of $n$ objects. In the case of the Ultra Lotto 6/58, one must choose $6$ numbers from a collection of $58$. Therefore, substituting these numbers to $r$ and $n$, respectively, yields the following: 

$$
_{58}C_{6} = \frac{58!}{6!(58-6)!}= 40,475,358
$$

<br>

After using the Combination Formula, we find that the amount of all possible combination of numbers is equal to approximately $40.5 \textrm{ million}$ combinations or tickets. 

At $P20$ per ticket, a bettor would have to spend an amount equal to the number of all possible combinations multiplied by the said price.

$$
\textrm{amount to spend}=P20 \cdot 40,475,358=P809,507,160 
$$
<br>

Purchasing tickets containing all combinations, the bettor will surely win the lotto prize of $P50 \textrm{ million}$. However, spending approximately a total of $P809.5 \textrm{ million}$ means that the bettor would incur a massive loss.

To find out how much exactly an individual can win in the 6/58, the rules of PCSO's Ultra Lotto 6/58 indicate that those who get 3/4/5 of the 6 winning numbers are eligible for a consolation prize. As of June 28, 2022, the PCSO consolation prize pool is as follows:

- 2nd place - 5 out of 6 winning nos. - $P120,000.00$
- 3rd place - 4 out of 6 winning nos. - $P2,000.00$
- 4th place - 3 out of 6 winning nos. - $P100.00$

*note that the current prize pool is $P49.50\textrm million$ but the prize pool in the scenario is $P5 \textrm million$. 
<br>

Since you bought all combinations, you will get the 442,000 tickets that got 3 out of the 6 winning numbers, which gives $P44,200,000.00$ .

$$
_{6}C_{3} \cdot [_{(58-6)}C_{(6-3)}]=442,000
$$

$$
442,000 \cdot P100.00= P44,200,000
$$

<br>

Do note that the 6/58 follows the pari-mutuel system pertaining to a betting pool in which those who win within the first three places share the total amount bet.

In case someone else but you wins a prize in the lottery, you will be splitting the top three prizes, effectively sinking you further in debt; but in case you are the sole winner, your total winnings would be $P94,322,000.00$ (without tax).

$$
\textrm{total winnings}=P50,000,000 + P120,000 + P2,000 + P44,200,000 = P94,322,000
$$

<br>

Regardless if you consider the consolation prizes ($debt_2$) or not $(debt_1)$, you will still be in enormous debt since neither of the outcomes would make you break even.

$$
\textrm{debt}_1= P809,507,160-P50,000,000=P759,507,160
$$
$$
\textrm{debt}_2=P809,507,160-P94,322,000=P715,185,160
$$

<br>
<br> 
Learn more about the Philippine Charity Sweepstakes Office or PCSO [here](https://www.lottopcso.com/).

  > Want to find out the Lotto results for today? Click [here](https://www.lottopcso.com/6-58-lotto-result).



---

#### <b>REFERENCES</b>
| 6/58 Lotto Result Today - Official PCSO Lotto Results. (2022). Retrieved 28 June 2022, from https://www.lottopcso.com/6-58-lotto-result/

\

| Chen, W. J., & Wang, J. T.-yi. (2020). A modified Monty Hall Problem. Theory and Decision, 89(2), 151–156. https://doi.org/10.1007/s11238-020-09757-1 

\

| Definition of pari-mutuel | Dictionary.com. (2022). Retrieved 28 June 2022, from https://www.dictionary.com/browse/pari-mutuel

\

| Monty Hall, Plinko, and Probability. The Game Theorists Wiki. (2012, July 26). Retrieved June 29, 2022, from https://matpat.fandom.com/wiki/Monty_Hall,_Plinko,_and_Probability 

\

| Numberphile (2014, May 22). Monty Hall Problem - Numberphile [Video]. Youtube. https://www.youtube.com/watch?v=4Lb-6rxZxx0&t=0s

\

| Vox (2015, December 1). The math problem that stumped thousands of mansplainers [Video]. Youtube. https://www.youtube.com/watch?v=ggDQXlinbME&t=0s



