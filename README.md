## Plan
### I - Poker - General Information
### II - Game Theory
- **1. Game Classification**
- **2. Optimal Strategies**
- .2.1: The Strategy of Eliminating Dominated Strategies (EISD)
- .2.2: Nash Equilibrium
### III - Poker Bots
- **1. Heads Up No-Limit Texas Hold'em Game Type**
- **2. Having a Strategy in Poker**
- **3. Nash Equilibrium, the Optimal Strategy**
- **4. Poker Game Tree**
- **5. History**
- **6. Online Poker & Bots**
### IV - Rock-Paper-Scissors with the CFR Algorithm
- **1. Principle of Counterfactual Regret Minimization**
- **2. Functioning of Rock-Paper-Scissors CFR**
### V - Kuhn Poker with Vanilla CFR Algorithm
- **1. Reminder of Kuhn Poker Rules**
- **2. Functioning of Kuhn Poker CFR**
- **3. Vanilla CFR**
### VI - Running the Algorithm on Microsoft Azure
- **1. Creating a Workspace**
- **2. Uploading and Cleaning Data, etc.**
- **3. Creating a Compute Instance**
- **4. Creating an Experiment + Script Execution Configuration + Submitting the Experiment**
- **5. Other Interesting Resources**
### VII - Monte Carlo CFR Algorithm
### VIII - Resources
- **1. To Understand the CFR Algorithm**
- **2. About Game Theory**
- **3. To Code a Vanilla CFR**
- **4. About Monte Carlo CFR & AI that Beat Poker Pros**
- **5. Other Interesting Resources on the Subject**
- **6. Running Deepstack for Leduc Poker on Your Computer**

---

# I - Poker - General Information

Poker is a family of card games.

Variants | Modes | Formats | Game Types | Tournaments |
|------|----------|-------|-------|-------|
| Texas Hold'em | Low | No limit (unlimited bets and raises) | cash game = players can leave the table and exchange chips for money | World Series of Poker |
| Omaha | High | Pot Limit (maximum raise equals the pot) | tournament = cannot convert chips into money, money is won by placing high in the tournament | World Poker Tour |
| Razz | High low | Limit | bounty tournament = when I eliminate a player, I win money | European Poker Tour |
| Stud || Half pot limit | sit and go | Asia Pacific Poker Tour |
| 5 Card Draw, ...|||| Latin American Poker Tour |

### No Limit Texas Hold’em, Basic Rules:

= played with cards and chips
= a 5-card combination game
= alternates between card distribution and betting rounds
= 52 cards, divided into 4 suits with 13 cards each, the strongest card is the Ace, the weakest is the 2
= 2 to 10 players
= heads-up = a match between only two players

Goal: win other players’ chips, be the last player with chips

**The Board** = the 5 cards placed on the table  
Objective: to have the best 5-card combination (7 cards in total)

- Royal Flush (10, J, Q, K, A + same suit)
- Straight Flush (sequence + same suit)
- Four of a Kind
- Full House (Three of a Kind + Pair)
- Flush / Color
- Straight / Sequence: Ace is the highest and lowest card
- Three of a Kind
- Two Pair
- One Pair
- High Card

**Buy-in** = minimum number of chips to play at a table  
**Dealer** = the one who shuffles and deals the cards  
**Small Blind (SB) and Big Blind (BB)** = players next to each other, rotate every hand, must bet (forces play), BB = 2x SB  
**Cut-off Player** = the previous dealer  
**Dealer (button)** = person distributing cards, counting chips, ensuring smooth gameplay, rotates every round  
**Kicker** = tie-breaking card  
**Buying in** = what you pay to enter a tournament  
**Bankroll** = reserved poker fund  
**Tells** = clues from players’ behavior  
**Fish** = novice player  
**Limp** = action to see the flop by paying the minimum (big blind)  
**Push/Fold Strategy** = limit your options to going all-in or folding  
**78o** = 7 and 8 offsuit  
**78s** = 7 and 8 of the same suit  

Detailed poker vocabulary dictionary [here](https://www.ludo9.com/poker/regles-poker/dictionnaire-poker/vocabulaire-poker-d/definition-dealer-poker/)

BB ---- SB ---- BUTTON

| 1. PREFLOP, betting round 1 | 2. FLOP + betting round 2 | 3. TURN + betting round 3 | 4. RIVER + betting round 4 | 5. SHOWDOWN |
|-----------------------------|-------------------------|-------------------------|-------------------------|-------------------------|
| SB and BB place their chips | Dealer burns a card + 3 face-up cards (Flop) | Dealer burns a second card + 1 face-up card (Turn) | Dealer burns a third card + 1 final face-up card (River) | At least 2 players reveal their cards. The winner takes the pot. |

# II - Game Theory

Theory of Games and Economic Behavior, John von Neumann and Oskar Mergenstern, 1944. Game theory is a branch of mathematics that provides practical tools for modeling and reasoning about interactive situations (games). Definition: Game theory allows for the formal analysis of problems posed by strategic interaction among a group of rational agents pursuing their own goals.

- Game theory **classifies games into categories** based on their resolution approaches
- **seeks to highlight optimal strategies** based on this classification

==> Since the 1980s, game theory has played an increasingly important role in computer science: applications in automata theory, logic, program verification, optimization, and reinforcement learning...

### 1. Game Classification

Interactive situations can vary widely depending on factors such as the number of players, utility structure, move order, etc. Based on these characteristics, we can classify games into types (e.g., zero-sum games, simultaneous games, sequential games, complete information games, incomplete information games, etc.)

Classification | Definition | Example |
|------|----------|-------|
| Zero-sum / Non-zero-sum | Zero-sum game = players' interests are strictly opposed. If players' preferences are represented by a gain function or utility function, the sum of both functions is always zero | Zero-sum: Rock-paper-scissors, Poker, Chess. Non-zero-sum: Prisoner’s dilemma (sometimes both players can lose). |
| Complete Information / Incomplete Information | Complete information: each player knows their possible actions, others' actions, and the outcomes of those actions. | Complete: Chess, Go. Incomplete: Poker, Tarot. |
| Perfect Information / Imperfect Information |||
| Finite Games / Non-finite Games | Finite games = players have a finite set of strategies. | Finite: Prisoner's dilemma. Non-finite: Cournot duopoly. |
| Cooperative / Non-cooperative Games |||
| 2-player Games / N-player Games |||

Notations:
- a set N of players N = {1, 2, ..., n}
- for each player i, a set of strategies Si = {s1, s2, ..., sni}
- for each player i, a utility function ui: S1 * S2 * ... Sn, associating gains to player i's strategies.

### 2. Optimal Strategies

A strategy describes how to act in all possible situations. A pure strategy of player i is an action plan prescribing an action for every situation where i may play.

**2.1: Strategy of Eliminating Dominated Strategies (EISD)**

| u | v | w |
|------|----------|-------|-------|
|x | 3,6 | 7,1 | 4,8 |
|y | 5,1 | 8,2 | 6,1 |
|z | 6,0 | 6,2 | 3,2 |

- The row player eliminates x, the column player eliminates u, and so on. The final solution (y, v) is Nash Equilibrium.

**2.2: Nash Equilibrium**
- An equilibrium where no player will change their strategy as it leads to worse outcomes if they deviate
- Does not imply maximal utility: it can be suboptimal
- A game can have multiple Nash equilibria
- [Video explanation](https://www.youtube.com/watch?v=wZAztwm4gI8)


# III - Poker Bots

### 1. Heads Up No-Limit Texas Hold'em Game Type

Heads Up No Limit Texas Hold'em Poker = an example of a two-person zero-sum finite game with imperfect information and chance moves.

### 2. Having a Strategy in Poker

Strategies must involve randomization, as deterministic strategies can be exploited.

**Behavioral Strategy** = complete action plan with probability distributions over actions at decision points.

### 3. Nash Equilibrium, the Optimal Strategy

The Nash equilibrium strategy in poker ensures you do not lose, and any deviation by your opponent increases their losses.

### 4. Poker Game Tree

Tic-tac-toe game tree:
![tictactoe_game_tree](https://user-images.githubusercontent.com/57531966/171430225-6d030585-7b2e-4b0b-9730-f030f80a9b19.png)

Kuhn Poker game tree:
![Poker_game_tree](https://user-images.githubusercontent.com/

57531966/171431519-8bc2061b-5553-4149-b834-28564afeb508.png)

### 5. History

- **2019**: Pluribus  
- **2017**: Libratus  
- **2015**: Claudico  
- **2015**: Cepheus  
- **2017**: DeepStackAI  
- **2007**: Polaris

==> All poker programs use **Counterfactual Regret Minimization (CFR)**.

### 6. Online Poker & Bots

Platforms like Pokerstars receive complaints about bots every month. Article [here](https://usbeketrica.com/fr/article/poker-en-ligne-les-bots-finiront-ils-par-chasser-les-humains).

# IV - Rock-Paper-Scissors with CFR Algorithm

### 1. Principle of Counterfactual Regret Minimization

Counterfactual regret = potential outcome regret. CFR minimizes regret over many iterations to approximate Nash equilibrium.

### 2. Functioning of Rock-Paper-Scissors CFR 

Players choose actions and track regret, updating their probabilities for future decisions. Over time, strategies converge to 1/3 for each action.

````
implementation at /Rock-Paper-Scissors/my_first_cfr_rockpaperscissors.py
````

# V - Kuhn Poker with Vanilla CFR Algorithm

### 1. Reminder of Kuhn Poker Rules

Simplified poker with only 3 cards and one betting round. The highest card wins.

### 2. Functioning of Kuhn Poker CFR

CFR works recursively through the game tree, calculating regrets for each action, updating strategies.

### 3. Vanilla CFR

````
implementation at /Kuhn-Poker/first_vanilla_cfr_kuhnpoker.py
````

Results after 25k iterations: the bot learns bluffing (betting with a low card) and inducing bets (passing with a high card).

# VI - Running the Algorithm on Microsoft Azure

Azure Machine Learning provides a platform to run machine learning workloads in the cloud.

### 1. Creating a Workspace

A workspace is a context for experiments, data, compute targets, etc.

Install the Azure ML SDK:
`````
pip install azureml-core
`````

````
from azureml.core import Workspace
ws = Workspace.create(name='aml-workspace', subscription_id='123456-abc-123...', resource_group='aml-resources', location='eastus')
````

### 2. Uploading and Cleaning Data

I have no data since the model trains by playing against itself.

### 3. Creating a Compute Instance

Go to the compute page, select a virtual machine, and start your instance.

### 4. Creating an Experiment + Script Execution Configuration + Submitting the Experiment

````
experiment_name = 'my_experiment'
experiment = Experiment(workspace=ws, name=experiment_name)
src = ScriptRunConfig(source_directory=project_folder, script='train.py', compute_target=my_compute_target, environment=myenv)
run = experiment.submit(config=src)
run.wait_for_completion(show_output=True)
```

### 5. Other Interesting Resources:
- [Video on no-code ML models](https://www.youtube.com/watch?v=TSEv5XN2keE)  
- [MOOC on AutoML](https://aka.ms/AutoML-MOOC)  
- [Microsoft Developer France YouTube channel](https://www.youtube.com/c/MSDeveloppeurs/videos)  

# VII - Monte Carlo CFR Algorithm

### 1. Main Concept of CFR: Regret

Regret expresses how much one would have gained with a different decision. CFR minimizes this regret over time.

### 2. No Regret Learning and Regret Matching Example

No-regret algorithms aim to minimize average regret over repeated iterations. Regret Matching adjusts weights on actions based on accumulated regret.

### 3. No Regret Learning & Game Theory

Repeated play of Rock-Paper-Scissors converges to Nash equilibrium using regret matching.

### 4. Average Regret

### 5. General Idea of MCCFR

CFR applied to imperfect-information games minimizes immediate counterfactual regret and converges to Nash equilibrium.

# VIII - Resources

### 1. To Understand the CFR Algorithm
- Introduction to CFR [document](https://github.com/iciamyplant/Poker/blob/master/Ressources/CFR/Introduction_to_CFR.pdf)  
- [Video](https://www.youtube.com/watch?v=NWS9v_r_IWk&t=1s)

### 2. About Game Theory
- [Two documents](https://github.com/iciamyplant/Poker/tree/master/Ressources/Th%C3%A9orie%20des%20jeux)

### 3. To Code a Vanilla CFR
- [Tutorial on Kuhn Poker](https://justinsermeno.com/posts/cfr/)

### 4. About Monte Carlo CFR & AI that Beat Poker Pros
- [DeepStack](https://github.com/iciamyplant/Poker/blob/master/Ressources/Poker%20IAs/DeepStack.pdf)  
- [Libratus](https://github.com/iciamyplant/Poker/blob/master/Ressources/Poker%20IAs/Libratus.pdf)

### 5. Other Interesting Resources
- [Introductory Video](https://www.youtube.com/watch?v=H5RA3NIDuDY)

### 6. Running Deepstack for Leduc Poker on Your Computer
- [DeepStack Github](https://github.com/lifrordi/DeepStack-Leduc)
