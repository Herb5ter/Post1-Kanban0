# Kanban Systems as a Display of Demand: A Combinatorial Perspective
## Introducing the Two-Bin Kanban System
In manufacturing, a two-bin Kanban system is a method of supplying materials by using an information card, called a Kanban card, as a signal to resupply a particular material. The word "kanban" means "signpost" in Japanese. 

When manufacturing processes convert raw materials into finished goods, there are bins that hold the various materials. As processes run, those bins are eventually emptied. In this Kanban system, each bin holds an information card about the particular material. When an empty bin is sent to a supplier, the supplier knows to send a full bin of the material to the manufacturer based on the card's description. Once the full bin is sent, the supplier also knows to produce more of that same material to remain in stock. This way, when the manufacturer empties the next bin of the same material and orders more from the supplier, the supplier can send the manufacturer the full bin in exchange for the empty bin. This process then repeats itself as the running time continues. 

Below is a diagram to depict a bin's movement between the manufacturer and supplier in the Kanban system.
<!-- As of August 2nd, 2026, nodes in differing subgraphs can link ONLY if the subgraphs have NO specified direction. -->
```mermaid
flowchart TB
  One(["Factory Floor"])-.->Act1["Bin empties."]--->|Empty bin sent to...|Two(["Material Production Location"]);
  Three(["Inventory"]) -.-> Act4["Material ordered by manufacturer."] --->|Material is sent to...| Four(["Inventory"]);
  Four -.-> Act5["Filled bin needed for manufacturing."]-->|Full bin sent to...|One
  subgraph Manufacturer
    One ~~~ Act1 ~~~ Act5 ~~~ Four
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
Since the Kanban card serves as a signal to the supplier that a particular material has been consumed and needs to be produced more of, we find that consumption drives production through the Kanban card. The Kanban card also signals demand for a particular material because the material is actively being requested for the manufacturing process.

+ _**<ins>Note</ins>**: From here through the rest of the article, the mention of "**process**" refers to a **manufacturing process**: a line-up of tasks that directly convert raw materials into finished goods._

Now, because a manufacturing facility may have multiple processes running at one time, it is possible that there are various scenarios of Kanban cards to be revealed for their respective materials. To better prepare for those scenarios, a facility may desire to know the possible structures of demand to encounter given the materials involved in each process. Knowing this requires us to ask this question:

>"How can the Kanban system be used to display possible structures of demand?"

## Assumptions For Representation
To delve into this question, let's establish some assumptions for our representation of a Kanban system.

1. Say that a factory holds a fixed number of various types of materials or parts, like bolts, nuts, gallons of paint, planks of lumber, and many others. Let's call this fixed number N.
2. Each of these N types of materials are available to readily contribute to any of the factory's manufacturing processes (from raw materials to finished goods).
3. Let's also assume that each process runs for the same predetermined process running time period, which is in some amount of hours, minutes, and seconds.
4. As each process empties bins for each material, assume that it has a full bin ready to be used (or drawn from) and the empty bin is immediately sent to the supplier.

_**<ins>Note</ins>**: For assumption #1, it's important to mention that each type of material has differing attributes, no matter how similar they are. For example, a 4" by 4" by 10' plank of pressure treated wood is a different material than a 4" by 4" by 15' plank of pressure treated wood._

### Consequences of Assumptions
Since this factory employs a two-bin Kanban system, then it's true that each of the N materials reveals a certain number of Kanban cards over the predetermined process running time period.

+ _**<ins>Note</ins>**: From now on, the words "running time", "time interval", or "time period" will refer to the "predetermined process running time period". Also, the words "card" or "cards" will refer to a "Kanban card" or "Kanban cards"._

Let's allow **$`c_i`$** to be the nonnegative number of cards that show from the use of the $`i^{\text{th}}`$ type of material during the time period, where $`i`$ is a whole number greater than 0 and less than or equal to N. (*Ex. If a 1/4' standard washer is material 1, and 5 cards show during the time period, then $`c_1`$ = 5 represents the Kanban cards for this particular washer during the time period.*)

Once we have a card count for all N types of materials, then we can add all of the card counts to obtain a number K, which is the total number of cards shown during the running time. As an equation, this statement shows $`c_1`$ + $`c_2`$ + ... + $`c_N`$ = K.

Now, the total K cards gives us a consumption notice of materials among the N types. Knowing this is crucial for counting possible demand results in the factory, especially since materials consumed in its processes indicate materials to be produced more of by the supplier. To find those demand results, we can ask "how many possible processes will reveal a specific amount of cards (like 6 cards, or 21 cards, etc.)"?

## Process Counting Reasoning
If there is a specified number of total cards, like K = 4, then we want to know how many possible card configurations will yield that specified number. We will define a card configuration to be one collection of card counts revealed for each type of material when the running time passes.

### Counting One Card Configuration
In the eyes of the supplier, the cards in the bins of each respective type of material (Ex. if 3 cards are revealed from material 4) are <ins>identical</ins> and <ins>indistinguishable</ins>.
* The cards are <ins>identical</ins> because the information on the cards for the material are about the same type of material. Each card is the same!
* The cards are <ins>indistinguishable</ins> because they can be switched around to appear in any order during the time period and the message to the supplier is to produce more of that type of material. No matter the order in which they appear to the supplier, the message to the supplier is the same!
<!-- **This perspective will be important later in this section! (may include this)**-->

Viewing from supplier's perspective of the cards, once the total K cards are split into the N groups of sizes $`c_1`$, ... , $`c_N`$ for the types of materials, we are able to count that splitting arrangement as a possible card configuration. If we begin with a line-up of all K cards, we can see that there are $`K - 1`$ spaces in-between the K cards, as shown below where one square represents a Kanban card.

$$
\displaystyle
{
  \Box \quad \Box \quad \dots \quad \Box \quad \Box 
}
$$

$$
\text{K cards}
$$


Placing a separator in one of the spaces allows us to divide the K cards into smaller groups. If there are N types of material, we can let one group represent one type of material. To split the cards into N groups, we will need $`N - 1`$ separators between the $`c_1`$, ... , $`c_N`$ groups. This is shown below.

$$
\displaystyle
{
  \Box \cdots \Box | \Box \cdots \Box | \cdots | \Box \cdots \Box
}
$$

$$
\text {K cards ( }\Box \text{ ), N groups or material types, and (N - 1) separators ( | )}
$$
+ _**<ins>Note</ins>**: Applying $`N - 1`$ separators to the total cards assumes that the sizes of each group are greater than 0, which is makes the values $`c_1`$, ... , $`c_N`$ not nonnegative, but only positive. For now, this assumption is necessary since it is easier to count groups that have cards in them compared to empty groups. This restriction will be relaxed later._

Once the separators are placed, then we have a possible card configuration, which is one possible consumption distribution of cards.

### Counting All Possible Card Configurations
Depending on where the separators are placed between, we obtain differing group sizes for the N types of materials. If we count the number of ways that each one separator can be placed in spaces between the cards, then we also count the number of possible differing group sizes for each type of material where each group is greater than 0 (for now). In turn, we also count the number of possible card configurations for a total of K cards.

Let's begin placing the separators! The $`1^{\text{st}}`$ separator has $`K - 1`$ possible locations for placement. The $`2^{\text{nd}}`$ separator has $`K - 2`$ possible locations for placement. This pattern continues through the $`(N - 1)^{\text{th}}`$ separator, which has $`K - (N - 1)`$ possible locations for placement. Since for every one placement of the $`1^{\text{st}}`$ separator, there are multiple placements for each of the other separators, the number of possible placement outcomes, and in turn card configurations, is given by

$$
\displaystyle
{
  (K - 1) \cdot (K - 2) \cdots \big(K - (N - 1)\big) \quad \quad \quad \text{ (1.1)}
}
$$

Now, since each separator has no distinction from the others despite their location of placement, there will be different outcomes that have the exact same card distribution among the types of material groups. An example of this is below for a process outcome with 3 total cards and 3 types of materials. Notice how the switch in separators, where one separator is a vertical bar "|" and another is a forward slash "/", creates the same splitting arrangement of cards.

$$
\Box | \Box  /  \Box \quad \quad \Box  /  \Box | \Box
$$

With only the expression in (1.1), we will count card configurations that have already been counted once. To avoid this, we must count the number of unique configurations only. Since configurations that present the same splitting arrangement are card outcomes that have separators in the same location, we can count then number of ways separators can be placed into those locations to obtain the number of exact outcomes for every one unique card configuration. 

With that, let's count the repeated outcomes! For the $`1^{\text{st}}`$ location of the separator, any of the $`N - 1`$ separators can be placed there. So, there are $`N - 1`$ possible results for the $`1^{\text{st}}`$ location. For $`2^{\text{nd}}`$ location, any of the $`N - 1`$ separators can be placed there other than the separator already placed in the $`1^{\text{st}}`$ location. So, there are $`N - 2`$ possible results for the $`2^{\text{nd}}`$ location. This pattern continues until the $`(N - 1)^{\text{th}}`$ location for the separator, which has only one possible result for the location.

We find that there are

$$
\displaystyle
{
  (N - 1) \cdot (N - 2) \cdots (2) \cdot (1) \quad \quad \quad \text{(1.2)}
}
$$

exact outcomes for every one unique card configuration.
* _**<ins>Note</ins>**: The symbol "!" is called a "factorial". The above expression reads "N minus one factorial". A whole, positive number with a factorial is the product of the initial number to all smaller whole and positive numbers. (Ex. 4! = 4 * 3 * 2 * 1 = 24)_

Because of this, dividing the expression (1.1) by (1.2) gives the number of unique configurations for the manufacturing process during the process running time, as shown below.

$$
\displaystyle
{
  \frac{(K - 1) \cdot (K - 2) \cdots \big(K - (N - 1)\big)}{(N - 1) \cdots (N - 2) \cdots (2) \cdot (1)} \quad \quad \quad \text(1.3)
}
$$

By multiplying the expression $`\frac{\big((K - 1)-(N - 1)\big)!}{\big((K - 1)-(N - 1)\big)!}`$ to (1.3), we can express the number of unique configurations as 

---

$$
\displaystyle
{
  \frac{(K - 1) \cdot (K - 2) \cdots \big(K - (N - 1)\big)}{(N - 1) \cdots (N - 2) \text{  } \cdots \text{  }(2) \cdot (1)}
  \cdot 
  \frac{\big((K - 1)-(N - 1)\big)!}{\big((K - 1)-(N - 1)\big)!}
}
$$

$$
\displaystyle
{
  = \frac{(K - 1) \cdot (K - 2) \cdots \big(K - (N - 1)\big) \cdot \big((K - 1)-(N - 1)\big)!}{(N - 1) \cdots (N - 2) \text{  } \cdots \text{  }(2) \cdot (1) \cdot \big((K - 1)-(N - 1)\big)!}
}
$$

$$
\displaystyle
{
  = \frac{(K - 1) \cdot (K - 2) \cdots \big(K - (N - 1)\big) \cdot (K - N)!}{(N - 1) \cdots (N - 2) \text{  } \cdots \text{  }(2) \cdot (1) \cdot (K - N)!}
    \quad \quad \Big(\text{substitute }\big((K - 1) - (N - 1)\big) \text{ with }(K - N)\Big)
}
$$

---

Since $`(K - N)! = (K - N) \cdot (K - N - 1) \cdot (K - N - 2) \cdots (K - K + 2) \cdot (K - K + 1)`$, we then have 

$$
\displaystyle
{
  (K - 1) \cdot (K - 2) \cdots \big(K - (N - 1)\big) \cdot (K - N) \cdot (K - N - 1) \cdot (K - N - 2) \cdots (K - K + 2) \cdot (K - K + 1)
}
$$

in the numerator of our fraction. Since N is always less than or equal to K, the numerator is equal to $`(K - 1)!`$. From here, we arrive to the following expression for the number of unique card configurations:

---

$$
\displaystyle
{
  \frac{(K - 1) \cdot (K - 2) \cdots \big(K - (N - 1)\big) \cdot (K - N)!}{(N - 1) \cdots (N - 2) \text{  } \cdots \text{  }(2) \cdot (1) \cdot (K - N)!}
}
$$

$$
\displaystyle
{
  = \frac{(K - 1)!}{(N - 1) \cdots (N - 2) \text{  } \cdots \text{  }(2) \cdot (1) \cdot (K - N)!}
}
$$

$$
\displaystyle
{
  = \frac{(K - 1)!}{(N - 1)! \cdot (K - N)!} \quad \quad \Big(\text{substitute }(N - 1) \cdots (N - 2) \text{  } \cdots \text{  }(2) \cdot (1) \text{ with }(N - 1)!\Big)
}
$$

$$
\displaystyle
{
  = \binom{K - 1}{N - 1} \quad \text{(1.4)}
}
$$

---

The final term representing the unique configurations is our counting expression, which in this case counts the number of process outcomes, or the ways to distribute the K cards among N types of materials. The counting expression can be read as "K minus one choose N minus 1". This expression is true when $`c_1`$ + $`c_2`$ + ... + $`c_N`$ = K where $`c_1`$, ... , $`c_N`$ are positive numbers.

Now, remember in the beginning of the "[Consequences of Assumptions](https://github.com/Herb5ter/Post1-Kanban0/edit/post1-RDedit/README.md#consequences-of-assumptions)" section where we said that each **$`c_i`$** term is a nonnegative whole number? We said this because not all types of material will have a card show in their group for all possible card configurations. In other words, some **$`c_i`$** terms will equal 0. So, how can our current counting expression represent something that has group sizes of positive values AND the value zero (a.k.a nonnegative values)?

Well, let's notice a few things about the our counting expression. First, our expression for the unique card configurations is true when $`c_1`$ + $`c_2`$ + ... + $`c_N`$ = K where $`c_1`$, ... , $`c_N`$ are positive numbers. Second, since each **$`c_i`$** term from our original reasoning in the "[Consequences of Assumptions](https://github.com/Herb5ter/Post1-Kanban0/edit/post1-RDedit/README.md#consequences-of-assumptions)" subsection is nonnegative, adding the value 1 to each of those terms will allow the nonnegative numbers to all be positive. 

So, if we make each **$`c_i`$** term in the equation $`c_1`$ + $`c_2`$ + ... + $`c_N`$ = K a nonnegative number, and if we add one to each of the group sizes for the types of material in the equation, then we obtain the following:

$$
\displaystyle
{
  c_1 + c_2 + \dots + c_N = K
}
$$
$$
\displaystyle
{
  (c_1 + 1) + (c_2 + 1) + \dots + (c_N + 1) = K + N \quad \quad \text{(add N ones to both sides of equation)}
}
$$
$$
\displaystyle
{
  S_1 + S_2 + \dots + S_N = K + N, \quad \quad \text{ where } S_i = c_i + 1 \text{ and } 0 \text{ } \textless \text{ } i \text{ } \leq N
}
$$

From here, we now have positive terms **$`S_i`$**, which have the same number of positive terms as the equation $`c_1`$ + $`c_2`$ + ... + $`c_N`$ = K. As a result, the two equations describe that same types of values, which means that the nonnegative group sizes $`c_1`$, ... , $`c_N`$ correspond to the counting expression 

$$
{\displaystyle
  {
    \binom{K + N - 1}{N - 1} \quad \text{(1.5)}
  }
}
$$
* _**<ins>Note</ins>**: Notice how "K + N" replaces the spot of "K" from the expression in_ (1.4).

This counting expression gives the total count of unique card configurations where card group sizes for the types of material can equal zero. To gain a more applied feel for this solution, let's approach an example. 

## Interpretation
### Example
Say we have 4 Kanban cards show up among processes that have 3 materials available for use throughout the factory. These materials are wood, screws, and paint. How many possible distributions of Kanban cards among the 3 types of materials are there?

First, let's imagine a few possible card configurations from the described process among the 3 material types. Some outcomes and their card line-ups include:
- 3 cards for wood, 1 card for screws, and 0 cards for paint

$$
\Box \Box \Box | \Box | \circ
$$

- 1 card for wood, 2 cards for screws, and 1 card for paint <!-- Include picture -->

$$
\Box | \Box \Box | \Box
$$

- 0 cards for wood, 0 cards for screws, and 4 cards for paint <!-- Include picture -->

$$
\circ | \circ | \Box \Box \Box \Box
$$

_**<ins>Note</ins>**: The circle_ ($`\circ`$) _represents a material showing no Kanban cards._

Because K represents the total number of Kanban cards that show during the process time and N represents the number of types of material the factory has available for use, we can say that $`K = 4`$ and $`N = 3`$. Since some of the card configurations have zero cards to show for some of the types of materials, we know that the amount of cards for wood, screws, and paint are nonnegative. So, if $`w`$, $`s`$, and $`p`$ are to represent the count of cards that show for wood, screws, and paint respectively, then 

$$
\displaystyle{w + s + p = 4, \text{ where w, s, p }\geq 0 \text{.}}
$$

We also know that the information cards that show within the groups for the wood, screws, and paint are _identical_ and _indistinguishable_. With this information and the counting expression in (1.5), the expression below will result in the count of possible unique card configurations.

$$
\displaystyle
  {
  \binom{K + N - 1}{N - 1} = \binom{4 + 3 - 1}{3 - 1} = \binom{6}{2} \text{.}
  }
$$

The fraction notation for the expression results in the following:

$$
\displaystyle
  {
  \binom{6}{2} = \frac{6!}{(6-2)!2!} = \frac{6!}{4!2!} = \frac{6 \cdot 5 \cdot 4!}{4!2!} = \frac{4!}{4!} \cdot \frac{6 \cdot 5}{2!} = 1 \cdot \frac{30}{2} = 15 .
  }
$$

There are 15 possible card configurations in this Kanban system where 4 cards show among any of the 3 material types.
### What does this mean?
The resulting number from the expression with the chosen Kanban card total 4 is the total number of ways that wood, screws, and paint can be consumed given the predetermined process running time. Because the cards are signals of production, and consequently the requested demand for the materials, this result gives the total number of <ins>**possible demand structures**</ins> for the factory in their manufacturing process over the running time. 

### How can this be helpful?
If a factory using a two-bin Kanban system knows what possible demand structures exist and how many, then decision-makers may be able to determine how likely it is for certain types of material to reach a certain consumption level during the running time period. Although I don't see how at the moment, our counting expression calculation may assist with predicting the requested demand of the types of goods before production processes begin. Probabilistic information on the each possible outcome of card arrangements in manufacturing processes would be helpful in prediction requested demand.

## Extending Questions
The question we began exploration with is "How can a Kanban system be used to display possible structures of demand?". From previous observations, the Kanban system can be used to show possible make-ups of demand, considering all available materials within a factory, by counting the total number of ways a specific amount of Kanban cards can show up among all available types of material to be used in a factory. 

- In this post, the Kanban system referred to is the two-bin system. However, during my reading, I found that there are many other types of Kanban systems like the Constant Work In Progress (CONWIP) system, the extended Kanban system, and the generalized Kanban system. How would the make-up of those systems change the make-up of our counting expression?

- Also in my reading, I learned about something called the Economic Order Quantity, which is the amount of materials/parts a company may order to minimize the cost of storing them for production. When a company is finding this measurement for a particular process, how does it impact the timing of Kanban cards showing in the production process?

- This representation does not consider the order of which the K cards distributed among the N groups appear during the manufacturing process. Considering the timing of cards revealing themselves during the time period, how would this representation change the number of possible card configurations?

These questions can be explored on a later date, as they will add on to the discussion about Kanban systems. To the reader, I appreciate your time given to read this exploration, and I will see you on the next post!
