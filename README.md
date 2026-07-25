# <!-- Title will show here; determine after draft is finalized -->
## About Section of the Post
<!-- WRite the about section after main secttions are finalized. Display this in the about section of the repository -->

## Introducing the Kanban System
In production processes, a kanban system is a method of supplying materials by using a kanban (means "signpost" in Japanese) card as a signal to resupply a particular material.

When materials are used to convert raw materials into finished goods, the bins that hold them are eventually emptied. In a kanban system, each bin holds an information card about the particular material so that when the empty bin is sent to a supplier, the supplier knows to produce more of that material based on the card's description. This way, when the manufacturer empties the next bin of the same material, the supplier can send the manufacturer the full bin in exchange for the empty bin. This process then repeats itself as the process operates. 

Below is a diagram to depict the system.
<!-- Kanban System DIagram here-->
When a manufacturer employs this system in production, they
- prevent excessive surplus of materials for production, and
- allow each process to have necessary materials for manufacturing.

## Question of Interest
Since the Kanban card serves as a signal to the supplier that a particular material has been consumed and needs to be produced more of, we find that <!-- May become a quote later. I want to emphasize this point.-->consumption drives production through the kanban card. The kanban card also signals a demand for a particular material or good because the kanban card's good is actively being requested for in the production process. 

Now, because a manufacturing facility may have multiple processes running at one time, it is possible that there are various scenarios of kanban cards being revealed for heir respective goods. To better prepare for those scenarios, a facility may desire to know the possible make-ups of demand they may encounter given the goods involved in each process. Knowing this requires us to ask this question:

>"How can the kanban system be used to display possible structures of demand?"

## Assumptions For Representation/Model <!-- Determine between one of these -->
To delve into this question, let's establish some assumptions for our representation of a kanban system.

1. Say that a factory holds a fixed number of various types of goods, like bolts, nuts, gallons of paint, planks of lumber, and many others. Let's called this fixed number N. It's important to mention that each type of good has a differing attribute about them, no matter how similar they are. For exmaple, a 4" by 4" by 10' plank of pressure treated wood is a different good than a 4" by 4" by 15' plank of pressure treated wood.
2. Each of these N goods are availible to readily contribute to any of the factories manufacturing processes (from raw materials to finished goods).
3. Let's also assume that each process runs for the same predetermined time period, which is in some amount of hours, minutes, and seconds.
<!-- Assumption 4 - To save or not to save. --> 
4. Even though each process may require different time intervals for process completion, a complete process is not necessary for this example. The reason why will be mentioned soon.
5. As each process empties bins for each good, assume that the good has a full bin ready to be used (or drawn from) and the empty bin is immediately sent to the supplier.

### Consequences of Assumptions
Since this factory employs a kanban system, then it's true that each of the N goods reveals a certain number of kanban cards over the predetermined time period. Let's allow **\c_i** to be the number of kanban cards that reveal as a the \i^th type of good is used over the the predetermined process time period, where i is a whole number greater than or equal to 0 and less than or equal to N. (Ex. If a 1/4' standard washer is good 1, and 5 Kanban cards are revealed during the predetermined process running time, the 
<!-- MAthe expression--> c_1 = 2 represents the knaban cards for this particular washer. 

Once we have a kanban card count for all N types of goods, then we can add all of the kanban card counts to obtain a number K, which is the total numbe rof knaban cards that are revealed in the predtermined process running time for all types of goods. As an equation, this statement shows 
<!-- Math expression--> c_1 + c_2 + ... + c_N = K

Now, we have N types of goods that contribute to any of the possible processes in the factory as as well as K kanban cards that are revealed for the goods as the processing running time period passes. SInce the kanban system cards signal consumption for each good, how many processes will reveal a specific amount of kanban cards (like 6 cards, or 21 cards, etc.)?

## Reasoning to Mathematical Solution <!-- Ponder on a another subtitle for this section -->
<!-- We'll stop here for today. Learn how to typeset mathematical solutions before continuing.>
