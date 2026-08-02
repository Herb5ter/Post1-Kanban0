# Kanban Systems as a Display of Demand: A Combinatoric Perspective
## Introducing the Kanban System
In production processes, a kanban system is a method of supplying materials by using a kanban card as a signal to resupply a particular material. The word "kanban" means "signpost" in Japanese. 

When materials are used to convert raw materials into finished goods, the bins that hold them are eventually emptied. In a kanban system, each bin holds an information card about the particular material so that when the empty bin is sent to a supplier, the supplier knows to produce more of that material based on the card's description. This way, when the manufacturer empties the next bin of the same material, the supplier can send the manufacturer the full bin in exchange for the empty bin. This process then repeats itself as the process operates. 

Below is a diagram to depict the system.
<!-- As of August 2nd, 2026. nodes in differing subgraphs can link ONLY if the subgraphs have NO specified direction. -->
```mermaid
flowchart TB
  One(["Factory Floor"])-.->Act1["Bin empties."]--->|Empty bin sent to...|Two(["Material Production Location"]);
  Three(["Inventory"]) -.-> Act4["Material ordered by manufacturer."] --->|Material is sent to...| Four(["Inventory"]);
  subgraph Manufacturer
    One ~~~ Act1 ~~~ Four
    end;
  subgraph Supplier
    Two -.-> Act2["Kanban Card is read."] ---> Act3["Empty bin filled."];
    Act3 --->|Bin placed in...| Three;
    end;
```
When a manufacturer employs this system in production, they
- prevent excessive surplus of materials for production, and
- allow each process to have necessary materials for manufacturing.

## Question of Interest
Since the Kanban card serves as a signal to the supplier that a particular material has been consumed and needs to be produced more of, we find that <!-- May become a quote later. I want to emphasize this point.-->consumption drives production through the kanban card. The kanban card also signals a demand for a particular material or good because the kanban card's good is actively being requested for in the production process. 

Now, because a manufacturing facility may have multiple processes running at one time, it is possible that there are various scenarios of kanban cards being revealed for their respective goods. To better prepare for those scenarios, a facility may desire to know the possible make-ups of demand they may encounter given the goods involved in each process. Knowing this requires us to ask this question:

>"How can the kanban system be used to display possible structures of demand?"

## Assumptions For Representation/Model <!-- Determine between one of these -->
To delve into this question, let's establish some assumptions for our representation of a kanban system.

1. Say that a factory holds a fixed number of various types of goods, like bolts, nuts, gallons of paint, planks of lumber, and many others. Let's call this fixed number N. It's important to mention that each type of good has a differing attribute about them, no matter how similar they are. For exmaple, a 4" by 4" by 10' plank of pressure treated wood is a different good than a 4" by 4" by 15' plank of pressure treated wood.
2. Each of these N goods are availible to readily contribute to any of the factories manufacturing processes (from raw materials to finished goods).
3. Let's also assume that each process runs for the same predetermined time period, which is in some amount of hours, minutes, and seconds.
<!-- Assumption 4 - To save or not to save. Hmmmm. --> 
4. Even though each process may require different time intervals for process completion, a complete process is not necessary for this example. The reason why will be mentioned soon.
5. As each process empties bins for each good, assume that the good has a full bin ready to be used (or drawn from) and the empty bin is immediately sent to the supplier.

### Consequences of Assumptions
Since this factory employs a kanban system, then it's true that each of the N goods reveals a certain number of kanban cards over the predetermined time period. Let's allow **$`c_i`$** to be the number of kanban cards that reveal as the $`i`$<sup>th</sup> type of good is used over the predetermined process time period, where i is a whole number greater than or equal to 0 and less than or equal to N. (Ex. If a 1/4' standard washer is good 1, and 5 Kanban cards are revealed during the predetermined process running time, then $`c_1`$ = 5 represents the kanban cards for this particular washer during the predetermined process running time.

Once we have a kanban card count for all N types of goods, then we can add all of the kanban card counts to obtain a number K, which is the total number of kanban cards that are revealed in the predetermined process running time for all types of goods. As an equation, this statement shows $`c_1`$ + $`c_2`$ + ... + $`c_N`$ = K.

Now, we have N types of goods that contribute to any of the possible processes in the factory as well as K kanban cards that are revealed for the goods as the processing running time period passes. Since the kanban cards signal consumption for each good, how many processes will reveal a specific amount of kanban cards (like 6 cards, or 21 cards, etc.)?

## Process Counting Reasoning <!-- Ponder on a another subtitle for this section -->
If there is a specified number of total kanban cards <!-- "like K = 4" -->, then we want to know how many possible outcomes of processes will yield that specified number of total kanban cards. We will treat the outcome of a process as the outcome of kanban cards revealed for each type of good after the predetermined process running time passes. 

<!-- You must breifly, simiply explain the combination concept and its notation BEFORE the next section.--->

### Counting of One Process
In the eyes of the supplier, the kanban cards that are revealed in the bins of each respective type of good (Ex. if 3 cards are revealed from good 4) are <ins>identical</ins> and <ins>indistinguishable</ins>.
* The cards are <ins>identical</ins> because the information on those kanban cards for the material are about the same type of goods. Each card is the same!
* The cards are <ins>indistinguishable</ins> because they can be switched around to appear in any order during the predetermined process running time and the message to the supplier is to produce more of that type of good. No matter the order in which they appear to the supplier, the message to the supplier is the same!

So, the total kanban cards K can be split in N groups of cards of sizes $`c_1`$, ... , $`c_N`$. This represents the cards that are selected to be revealed in each bin for the types of goods.

Then, to select $`c_i`$ identical cards for the bins of the $`i`$<sup>th</sup> type of good from the corresponding $`c_i`$ groups of kanban cards such that they are indistinguishable, the number of ways to select the cards is <!-- c_i C c_i; Use Latex/MathJax for this --> for each bin of the $`i`$<sup>th</sup> type of good. 

Consequently, to represent one process, which is the distribution of kanban cards among each material, we have
<!-- Mathematical expression on page 15a -->
as the number of ways to distribute K cards among N types of goods for the kanban system for one process.

### Counting of All Possible Processes
To count all possible processes based on the total N materials in the factory, we must count all kanban placement scenarios where the sum of cards placed in the bins is K. This is can be found with following expression:
<!-- Mathematical Expression on page 15b -->,
which is the sum of all possible expressions of the form <!-- Mathematical expression on page 15a --> where $`c_1`$, ... , $`c_N`$ are nonnegative integers and their sum equals K. 

The above expression is a general way of counting the possible number of processes given some usage of the types of goods. To make this expression a little more intuitive, interpreting an example will be helpful.

## Interpretation
### Example
Say we have 4 kanban cards show up among processes that have 3 materials availible for use throughout the factory. These materials are wood, screws, and paint. How many possible ways can we expect the kanban cards to reveal themselves as they are used?

One possible process can show 2 kanban cards for wood, 1 card for screws, and 1 card for paint. For this process, we can ask these questions for each group of kanban cards:

- "How many ways can 2 identical, indistinguishable information cards for wood show upin a group of 2 to result in different production outcomes?"
- "How many ways can 1 identical, indistinguishable information card for screws show up in a group of 1 to result in different production outcomes?"
- "How many ways can 1 identical, indistinguishable information card for paint show up in a group of 1 to result in different production outcomes?

The answer to each of these questions is 1 way. 

Using combinations, this one process is expressed as the number <!-- Math Expression on page 16a --> .

There are many other processes that have 4 cards show up among the types of goods. Other examples include, but are not limited to,...
- 3 cards for wood, 1 card for screws, and 0 cards for paint
- 1 card for wood, 2 cards for screws, and 1 card for paint
- 0 cards for wood, 0 cards for screws, and 4 cards for paint

The total number of processes where 4 Kanban cards are found in the 3 types of goods adds all of the processes like the ones previously listed. The expression to represent this sum is 
<!-- Mathematical Expression on page 16b --> 
, where $`c_1`$, $`c_2`$, and $`c_3`$ are the number of cards for the first type of good (wood), second type of good (screws), and third type of good (paint) respectively. The sum of $`c_1`$, $`c_2`$, and $`c_3`$ is 4.

### What does this mean?
The resulting number from the sum of all possible processes with the chosen kanban card amount K is the total number of ways that the types of goods can be consumed given the predetermined process running time. Because the kanban cards are signals for production, and consequently the requested demand for the materials, this result gives the total number of <ins>**possible demand structures**</ins> for the factory in their manufacturing process over the predetermined process running time. 

### How can this be helpful?
If a factory using a Kanban system knows what and how many possible demand structures exist, then decision-makers may be able to determine how likely it is for certain types of goods to reach a certain concumption level during the prdetermined process running time period. When determining liklihoods of such consumption events, I imagine that this calculation will determine the basis from which the events can come from. Although I don't see how at the moment, the calculation may assist with predicting the requested demand of the types of goods before production processes begin.

## Extending Questions
The question we began exploration with is "How can a Kanban system be used to display possible structures of demand?". From previous obeservations, the Kanban system can be used to show possible displays of demand by counting the total number of ways a certain amount of kanban cards can show up among all availible types of goods to be used in a factory. 

- In this post, the Kanban system referred to is the two-bin system. However, during my reading, I found that there are many other types of Kanban systems like the Constant Work In Progress (CONWIP) system, the extended kanban system, and the generalized kanban system. How would the make-up of those systems change the make-up of our counting expression?

- Also in my reading, I learned about something called the Economic Order Quantity, which is the amount of goods a company may order to minimize the cost of storing good for production. When a company is finding this measurement for a particular process, how does it impact the timing of kanban cards showing in the production process?

We may explore these questions on a later date, as they may add on to the discussion about Kanban systems. To the reader, I appreciate your time given to read this exploration, and I will see you on the next post!
