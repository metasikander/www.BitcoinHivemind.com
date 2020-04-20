# Truthcoin
**Peer-to-Peer Oracle System and Prediction Marketplace**  
*Paul Sztorc[^1]  
truthcoin@gmail.com  
[https://github.com/psztorc/Truthcoin](https://github.com/psztorc/Truthcoin)  
1M5tVTtynuqiS7Goq8hbh5UBcxLaa5XQb8  
Version 1.5 - 12/14/2015*

**Abstract.** Bitcoin can support financial derivatives and smart contracts, but the main benefits are lost if a trusted third party is required to inform these contracts. Instead, I propose a proof-of-work sidechain which collects information on the creation and state of Prediction Markets (PMs).

An “oracle corporation” model attempts to guarantee that a group of self-selected, anonymous, greedy users will always resolve contract-outcomes honestly. Outcomes are established by weighted-vote, according to users' ownership of a second type of "VoteCoin", of which there are a constant amount (granting Sybil-immunity). Ownership of the VoteCoins is redistributed according to a Schelling Coordination Game, which destabilizes malicious cartels only. Large individual malicious-votes are discouraged through [1] collapse in the market value of Votecoins and [2] threat of (rare, Sybil-resistant) Miner Vetoes and Overrides. Like equities, VoteCoins are tradable and pay dividends over time, removing the incentive for an "exit scam".

Users [1] bear all of the economic costs and benefits of any PMs they create (ensuring efficiency), [2] can create PMs on any subject, and [3] can trade anonymously in any PM. All PMs enjoy low fees, permanent market liquidity, automatic token-issuance, and fair, high-speed trading through a LMSR market maker. Scalability and customizability are achieved via ‘branching’ (controlled-fork of the VoteCoin set).

PLEASE send Typos/Confusions to [truthcoin@gmail.com](mailto:truthcoin@gmail.com) or pull request into the following link: [https://github.com/psztorc/Truthcoin/tree/master/docs#addendum--errata](https://github.com/psztorc/Truthcoin/tree/master/docs#addendum--errata) (And check the link for a preview of later version)

## Article I. Overview
### (a) General Strategy
#### (i) Central Facts
##### 1) Blockchains allow for the programmable, censorship-resistant exchange of value-tokens.
##### 2) While most marketplaces require physical infrastructure to facilitate the trade of physical goods [^2] , a Prediction Marketplace requires only the trade of digitizable information, and can therefore exist entirely in a software environment.
##### 3) As time progresses, questions which were previously mystifying become easier and easier to answer. For example, the question “Will Candidate X win the November 2016 US presidential election?” may be impossible to answer in 2015, easier to answer in late October 2016, and very easy to answer in December 2016.
#### (ii) Assumptions
##### 1) Truthcoin inherits all of the assumptions of Bitcoin. For example: No malicious entity (an individual or perfectly-coordinated group) controls a large percentage of hashing power.
##### 2) Users are greedy (prefer having more money to having less money), and lazy (prefer putting in low effort to high effort).
##### 3) Miners might care (ie, “care with some difficult-to-measure but nonzero probability”) enough about the transaction fees derived from the Truthcoin sidechain to (as a very rare last-resort) act purposefully on behalf of the coin. This may be, for example, to cast a single “Veto” for Ballots which contain large sets of mis-resolved Decisions.
#### (iii) Scope
##### 1) Initially, this project aims to address public topics which are very easy to verify: no more than two minutes of web searching to resolve each “Decision” (“Decisions” partition the Prediction Markets (PMs)). Over time, Truthcoin is designed to be able to address topics of ever-increasing obscurity (see Article III “Branching”).
### (b) Brief Overview of Components
#### (i) The Two Coin-Types
##### 1) The Truthcoin blockchain is a Satoshian proof-of-work blockchain [^3] with different block-creation/validation rules. Most distinctively, Truthcoin uses two types of coin: “CashCoins” (CSH) and “VoteCoins” (VTC).
###### a) CashCoins are most relevant to the user: They are redeemable 1:1 for Bitcoin [^4] , and represent value. CSH-owners can make use of the protocol’s features (create PMs, and buy/sell/transfer PM-shares), without owning/worrying-about VoteCoins at all.
###### b) VoteCoins are a new type of coin unique to Truthcoin, and represent [^5] equity in the “oracle corporation”. The introduction of this second coin-type achieves many things. First, it provides a sharp definition of the fuzzy concept of “reputation”. Second, it makes “reputation” tradable, such that users can buy and sell this resource in precisely the same way that they might purchase shares of a real world corporation. This fixed amount of “tradable reputation” has many benefits, the chief of which are [1] Sybil-attack immunity, and [2] the alignment of ownership and control (economic value added/destroyed translates directly to an economic reward/penalty). Third, it gives the system a way to penalize agents (by withdrawing their VTC) for laziness. Fourth, it eliminates the temporal dimension from all incentive calculations (payments can be compared with each other, regardless of when they take place); if not eliminated, this dimension would have presented catastrophic risks (namely, the “exit scam” [^6] ).
####### i) Truthcoin can host many “oracle corporations”, which are called “Branches”, and each Branch has its own set of VoteCoins. A higher percentage of VoteCoins owned implies a greater degree of voting influence within the Branch, and a larger share in the Branch’s revenues.
####### ii) VoteCoins do not interfere with the digital-scarcity of Bitcoin/CashCoins. As a store of value, VoteCoins are inferior to CashCoins, because VTC-owners are obligated to “vote” on a certain number of Outcomes, making a VoteCoin address more “employee ID” and less “checking account number”.
####### iii) VoteCoins are used to perform labor in the “oracle corporation”, in a weighted-voting system.
######## a. VoteCoins allow (“require”) Owners to vote on the Yes/No/Scalar/Unknown status of ‘Decisions’ (questions whose answers are eventually “measureable at low cost”).
######## b. VoteCoins allow one to proportionally collect (in CashCoin) [1] Listing Fees, and [2] half of the marketplace Trading Fees.
####### iv) Ownership of VoteCoins may change, solely based on voting activity.
######## a. VoteCoins are lost if Owners refuse to vote, or if Owners cast votes differing from the multivariate plurality (usually, the “majority”).
######## b. VoteCoins are gained if Owners vote on neglected Decisions (those with few votes), or if Owners vote with the multivariate plurality on disputed Decisions (those where the Outcome was not unanimous).
#### (ii) Automated Market-Maker
##### 1) Literally, a protocol for updating market prices based on trading activity, [^7] which aims to replace the complicated technical matching algorithms (and supporting infrastructure) of modern financial markets with a single sequence of atomic state-updates.
##### 2) Figuratively, a “trader” who:
###### a) Utilizes LMSR technology [^8] [^9] to take the other side of any and all PM-trades, ensuring market liquidity (such that markets have a tradable market price at all times [even when volume and open interest fall to zero]). Low liquidity has been a problem on many PM-implementations, cryptocurrency or otherwise, and may have prevented the formation of crucial network-effects.
###### b) Has blockchain-properties (constant mining, P2P network) which allow for an always-on, high-speed, censorship-resistant trading environment.
###### c) Understands the creation (pre-trading, pre-event), maturation (post-event) and closure (post-event, post-trading) of Markets.
###### d) Collects, stores, and pays out funds, without human-error or mismanagement.
#### (iii) (Claims about the) Incentive Mechanism
##### 1) Authors
###### a) Any user can create a prediction market (“Author a Market”) about anything.
###### b) Authors only have an incentive to write Decisions whose outcome (they believe) will be, by a certain date, confidently known to Voters.
###### c) Authors only have an incentive to create Markets if they anticipate sufficiently-high trading volume (i.e. the contentious issues which would most-benefit from a prediction market).
###### d) In all Markets where liquidity would be valued by Traders, Authors have an incentive to endow new Markets with an optimal amount of initial liquidity.
###### e) Authors completely avoid the (prohibitive) cost of convincing Traders of their trustworthiness.
##### 2) VoteCoin Owners (“Voters”)
###### a) Voters have an incentive to maximize the long-run trading volume of future PMs on their Branch, which encourages them to establish and maintain a reputable network.
###### b) Voters have an incentive to participate in the resolution of all Decisions.
###### c) Voters have an incentive to vote “the way they believe other Voters will vote”, which itself is contrived to be “an accurate description of reality” (see ‘[Voting Strategy’).
##### 3) Traders
###### a) Any CashCoin user can trade on any PM without directly interfacing with VoteCoins at all. VoteCoins are the “employee layer”, not the “customer layer”.
###### b) Traders have an incentive to set the market price to “their personal expectation of the probability of the event taking place”, revealing that information to the public. For Scaled Decisions (on financial asset prices, for example), this trading activity produces an accurate and robust price feed.
###### c) Traders enjoy an absence of counterparty risk (but instead must endure the technical risk inherent to new Blockchain technology).
##### 4) Bitcoin Miners
###### a) Miners always have an incentive to mine blocks, as the marginal cost for doing so is zero (merged mining allows reuse of Bitcoin hashes). Were Bitcoin to disappear, the marginal cost/benefit of Truthcoin-mining would equal that of Bitcoin-mining (and mining would therefore continue).
###### b) Miners have an incentive to include every trade and transaction into a block, as this maximizes not only transaction fees, but also dividend revenue and therefore market capitalization of the coins. Miners cannot even read Markets or Votes until they have already been included in blocks, making this process censorship-resistant.
### (c) Extensible (Scalable, Customizable) Design
#### 1) Accompanying software [^10] is open source.
#### 2) Truthcoin allows for the creation of controlled forks of the VoteCoin set (‘Branches’) enabling growth of the scope and quantity of Markets, specialized judging, choice of different fee and timing parameters, etc. 
## Article II. How it Works
### (a) Truthcoin Blockchain and Coin Types
#### 1)
The Truthcoin blockchain is a Bitcoin-inspired proof-of-work blockchain which aims to impose different block validation rules on the original Satoshian cryptosystem. While the Bitcoin blockchain is designed only to hold information about the ownership and transfer of a single coin-type, the Truthcoin blockchain is designed to contain information about the transfer of three coin-types (CashCoins, VoteCoins, and Shares [^11] ), as well as the existence and state of Prediction Markets.

#### 2)
The Truthcoin blockchain contains a new type of coin called a “VoteCoin”:  
|   | CashCoins (“Bitcoin”) User-Layer | VoteCoins (“Reputation”) Employee-Layer |
|:-:|:-:|:-:|
| 1 | Coin values are analogous to a saved quantity of gold. | Coin values are analogous to reputation, influence, or shares of a corporation. |
| 2 | Without user input, account balances do not change. | Accounts may either gain or lose unspent coins (based on voting activity). With no user input, coin balances would decrease. |
| 3 | Private keys sign messages that [1] transfer value, [2] create prediction markets, and [3] trade in those markets. | Private keys only sign Votes (which influence the Outcomes of Decisions) or messages which transfer VoteCoins. |
| 4 | To mimic the experience of gold and provide an objective initial distribution of coins, new coins are periodically introduced in each block by miners, asymptotically approaching 21 million total coins.[^12] |
| 5 | Expectation of huge number of addresses, one per value transaction. | Expectation of a maximum of 10,000 addresses, all of which will vote, but few of which will transact. |

### (b) (Decentralized, Incentive-Compatible) Calculation of Decision Outcomes
#### (i) Terminology
##### 1)
**CashCoins** – A cryptocurrency which is functionally equivalent to Bitcoin, yet with the ability to interface with Truthcoin prediction markets.  

TODO: image from page 7  

Figure 1. Graphical representation of Truthcoin’s structure. Notice the two types of coin (circles), the VoteCoins representing reputation (top, colored) and the CashCoins representing money (bottom, grey). Decisions can either be Binary (bordered) or Scaled (blurred). When used in Markets, Scaled Decisions span an entire dimension, whereas Binaries only partition-from-null.  

##### 2)
**Decisions** – Questions that must be resolved by Voters. These partition the State-space of a prediction market, and are defined by items such as ‘event text’, ‘event date’, ‘tags’, ‘author’, etc. (see Appendix IX).  

###### a) Truthcoin supports two ‘types’ of Decision:
####### i) Binary (Boolean) Decisions: TODO: Add mathematics
######## a. Example 1: “Will Hillary Clinton be elected US President in 2016?”
######## b. Example 2: “Will the NYSE:DJIA closing price ever rise above 20,000 USD/Share in 2017?”
####### ii) Scaled (Scalar) Decisions: TODO: add mathematics
######## a. Example 1: “How many Electoral College votes will Hillary Clinton receive in the 2016 US Presidential election (if Hillary does not run, select ‘zero’)?” TODO: add mathematics
######## b. Example 2: “What will the NYSE:DJIA closing price be on January 1 st , 2018 (USD/Share)?” TODO: add mathematics
######## c. must be set in advance. Having a Decision expire at or near a bound has slightly adverse economic consequences for the Author of any Market using this Decision. TODO: add mathematics
###### b)  State “.5” denotes that a Decision is excessively confusing/irresolvable/unobservable (its veracity cannot easily be measured). This has adverse economic consequences for the Decision’s Author.
###### c) At any given time, each Decision will have a ‘status’ of one of the following:
####### i) Active: The Decision has just been created. Decisions of the ‘active’ status would be likely to be used to create Markets, and those Markets would be actively traded.
####### ii) Matured: Decisions contain a ‘date by which the information will become available’. After this date has passed, the Decision has a status of ‘matured’, and will enter the next Vote Matrix and be Voted on for resolution.
####### iii) Disputed: If Voters cannot sufficiently agree on the Decision’s outcome, the Decision remains un-resolved and gains this status. From here it will be Audited.
####### iv) Vetoed: If Miners veto the Decision’s Ballot, it gains this status (regardless of Voterbehavior).
####### v) Resolved: If Voters do sufficiently agree on the Decision’s outcome, and the Ballot is not Vetoed, their agreed-upon value becomes the final value of the Decision, and the Decision’s life-cycle is now over.
##### 3)
**Markets** – The lifeblood of the Truthcoin project, Prediction Markets allow anyone with CashCoin to buy and sell shares representing states of the world, and thereby speculate on and profit from selected events. This voluntary “win-win” speculation aggregates and summarizes information for use by the public.  

###### a) States: Markets partition the world into ‘states’ or “mutually-exclusive possible descriptions of reality”. When traders buy and sell shares, these shares are of a single Market State.
###### b) Status: Markets exist in one of two statuses:
####### i) Trading: In this status, a Market allows traders to buy and sell shares through an automated market-maker. A Market would be in this status from the moment it is created until all of its Decisions are voted on.
####### ii) Closed: When all of the Market’s Decisions are successfully resolved, the Market can be “closed” with a special message, which disables buying and replaces selling with redeeming.
TODO: add image on page 9

Figure 2. Graphical representation of three Prediction Markets, each with Binary Decisions. Left, the simplest form popularized by InTrade, with one dimension (blue dashed arrow), one Decision (red circle), and two states (yellow squares). Center, a Market with not two but four mutually exclusive states (for example, the winner of a 4-team tournament) and three Decisions. Right, a prediction market with two dimensions. Multidimensional prediction markets [^13] allow users to trade not only on the probability of each state, but also the relationship between dimensions [^14] , such as the relationship between an election result and the achievement of an economic goal a year later[^15].

##### 4)
**Branches** – Although all Markets are globally available to all users, Decisions are partitioned into clusters called ‘Branches’ based primarily on topic. Each Branch has its own set of VoteCoins (and therefore Voters), its own Decisions, and its own parameters (see Appendix IX).  

##### 5)
**VoteCoins** – The second cryptocurrency type in Truthcoin. Unlike CashCoins, VoteCoins are a liability as well as an asset. Owners are expected to use their coins to vote honestly on the Outcome of each Decision (or lose them).  

##### 6)
**Intervote Period (“Tau”)** – The length of time between two consecutive votes on the same Branch.  

##### 7)
**Vote** – The value which a Voter believes would match a given Decision to its real-world Outcome. The default value is “Missing”, which indicates “No response from the Voter”. A value of “1” would indicate “TRUE”, “0” would indicate “FALSE”, and “.5” would indicate “I can’t easily tell” or “breaks the Branch rules”).  

##### 8)
**Ballot** – The set of all matured Decisions on a Branch. For each Decision in a Ballot, every Voter must cast a Vote with his report/opinion on the resolved value. Notice that Ballots are defined by the maturation time of their Decisions, not by their organization or use within Markets (and, crucial to the core design, Ballots contain the Decisions of many different Markets).

##### 9)
**Vote Matrix** – The matrix created by stacking the Ballots (of a particular voting cycle) by -row. The columns of the matrix correspond to Decisions.

CONT! PAGE 10  

[^1]: Dedicated to Robin Hanson, for [taking the high road.](http://www.overcomingbias.com/2013/05/high-road-doubts.html)  
[^2]: [https://www.lme.com/trading/warehousing-and-brands/warehousing/approved-warehouses/](https://www.lme.com/trading/warehousing-and-brands/warehousing/approved-warehouses/)  
[^3]: [https://bitcoin.org/bitcoin.pdf](https://bitcoin.org/bitcoin.pdf)  
[^4]: [http://www.blockstream.com/sidechains.pdf](http://www.blockstream.com/sidechains.pdf)  
[^5]: The analogy is imperfect. The chief difference is that, in this “corporation”, owners are employees and vice-versa.  
[^6]: [http://motherboard.vice.com/read/darknet-slang-watch-exit-scam](http://motherboard.vice.com/read/darknet-slang-watch-exit-scam)  
[^7]: [https://github.com/psztorc/Truthcoin/raw/master/docs/LogMSR_Demo.xlsx](https://github.com/psztorc/Truthcoin/raw/master/docs/LogMSR_Demo.xlsx)  
[^8]: Original Publication: [http://mason.gmu.edu/~rhanson/mktscore.pdf](http://mason.gmu.edu/~rhanson/mktscore.pdf)  
[^9]: Clarifying Excel Spreadsheet: [http://www.truthcoin.info/papers/LogMSR_Demo.xlsx](http://www.truthcoin.info/papers/LogMSR_Demo.xlsx)  
[^10]: [https://github.com/psztorc/Truthcoin](https://github.com/psztorc/Truthcoin)  
[^11]: That which is “worth $1 if Candidate X is elected”, (the Arrow–Debreu securities themselves).
[^12]: I refer, of course, to the origin of these sidechained CashCoins: the Bitcoin Blockchain.  
[^13]: [http://www.truthcoin.info/papers/2_PM_Types.pdf](http://www.truthcoin.info/papers/2_PM_Types.pdf)  
[^14]: [http://www.overcomingbias.com/2008/07/intrades-condit.html](http://www.overcomingbias.com/2008/07/intrades-condit.html)  
[^15]: [http://www.overcomingbias.com/2008/01/presidential-de.html](http://www.overcomingbias.com/2008/01/presidential-de.html)  