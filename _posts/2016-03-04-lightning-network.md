---
title: A Lightning Network for Hivemind
comments: true
author: true
---


### Problem


Bitcoin and Truthcoin are too different for the original Lightning Network proposal to work. One huge disadvantage: Bitcoin has just one dimension, whereas Truthcoin would have one per market-state. That's not a big deal.

A bigger problem is the incentive-structure of Truthcoin -- it involves a third party (the Oracle.). Truthcoin will only work, if we can guarantee that agents will always get paid for (exactly) the services they provide.

Truthcoin has a Distributed Oracle "Corporation", which pays employees for their honesty. These payments come from traders. However...if trades are being moved off chain, how are we to get 'the chain' to figure out "how much to bill the traders" (for their trading)!


### Basics


We'll start with a simple example, to solve the "dimensions" problem.

We can create something similar to the capital markets of today. In these markets, users [1] deposit cash into a commercial bank, [2] transfer that money into a brokerage account, and then [3] make trades by interacting with a brokerage.

To replicate that in HM, we will use the LMSR for issuance. Then, trades among issued shares will be linked to a market through a bidirectional channel.

First, I'll sketch out a per-market channel.


## Swapping Shares for BTC

1. Someone (Person "A") spends a lot of money on an on-chain tx. This tx buying Q=100,000 shares, of each and every state of a market ("M1"). This will always cost Q BTC in working capital + Q * trading_fee + one transaction fee.
2. A advertises that he is going to become a "hub" for Market M1.
3. Regular users (B1, B2, ... Bn) connect to A, by setting up a payment channel between them:

    Inputs: 
        A's shares of State 1, State 2, ... of Market M1.
        B's cash.

    Outputs:
        A's Cash account.
        B's Cash account.
        A's shares of State 1, State 2, ... of Market M1.
        B's shares of State 1, State 2, ... of Market M1.
        M1 trading fee's account.

Both get a refund transaction, refunding everything they put in, which is valid after T=2 months (or whatever). The refund transaction has priority zero (ie, it will be replaced/updated, ...in the parlance of the LN whitepaper it "has not (yet) been invalidated").

4] A and B communicate, off blockchain, whenever they like, to update the transaction.

For example, they might have started with:

    Input: B pays 100 cash, A pays 100 shares each of M1:1 and M1:2.

    and

    Output: B gets 100 cash, A gets 100 shares each of M1:1 and M1:2.  [Priority 0]

Which can then be updated to:
    
    Output: B gets 99.5 cash, 0 shares of M1:1, and 2 shares of M1:2. A gets 0.5 cash, 100 shares of M1:1, and 98 shares of M1:2. [Priority 1]

Some time after that, the may update again:
    
    Output: B gets 94.5 cash, 3 shares of M1:1, and 2 shares of M1:2. A gets 5.5 cash, 97 shares of M1:1, and 98 shares of M1:2. [Priority 2]


This simple example demonstrates that trading can still happen within one on-chain message. The only requirement is that the dimensions are pre-selected.

To address this requirement, trading might start with large (kb) messages (of many pre-selected share-dimensions), and, just before broadcast, reduce to a smaller message (one which excludes share-dimensions which were never transacted in). In this way, both parties may agree to update to a smaller (economically-equivalent) message.


## Enforcing the Trading Fee

Now, on to our second, and more important, difference between HM and BTC: free-riding on a third party.

First, we have some advantages:

* The existing "hash locked" contracts, of the original LN, already allow BTC to hop over from Bitcoin world to Truthcoin world, without (even) going through a two-way peg (a 2wp must exist, but we are unhindered by it's lengthy clearing periods).
* In Bitcoin's "cash universe", everyone earns and spends money. However, in this model, only a few individuals will have any funds at all, and they will only want to trade in a few markets.
* A 'hub and spoke' model is comparable to the traditional capital market trading experience, and allows the "hubs" to compete on fees, uptime, etc.
* A 'hub and spoke' construction means that the *trading* channels will never need to span more than one individual. If a hub goes down, individuals can cancel their position by opening a new channel with a different hub, and buying a set of mutually-exclusive shares.


Let's get started!

### Basic Rules

First, I'll restrict the movement of share-tokens (but not Bitcoin, of course) to two places: [1] "the" MSR of the Market, and [2] in a payment channel. This means: no sending to a friend, no multisig, no locktime, no sending to yourself, etc. If you want to *store* your wealth, just use the LN to hop out of the Hivemind sidechain and back into Bitcoin (which you can do at any time).

Now that we've cornered the share-tokens, and coralled them into our special 'channel' message-type, we can see if we can force them to do accurate bookkeeping.


### Strategy

Our strategy is similar to the original LN: allow two parties to create new asset-allocation(s) "at will", and allow parties to invalidate old allocations, such that any non-conformity results in all funds being dramatically stolen.

However, in this case, the two parties have a mutual interest in defrauding the oracle. Instead of paying fees with each trade, they could simply wait for all of their off-chain trades to be finished (potentially, millions of them), and then simply pay one trading fee (on the net balance of the million trades).

This has undesirable effects: [1] if there is no selling, total trading fees will always be a tiny percentage of open interest, [2] it causes lower overall fees, which encourages the magnitude of the fee-parameter to rise, creating additional trade frictions and dead-weight losses. It makes the (intended) "trading" fee more of an "open interest" fee.

So, we will need to force each off-chain transaction to [1] calculate, [2] pay, and [3] aggregate the correct trading fee, such that the grand total is correctly calculated / paid when the full transaction is broadcast.

As with original LN, we'll have to **give** the counterparties an incentive to "rat" each other out, to the blockchain (because, as it stands, they collectively have the *opposite* incentive) if either one screws up the calculation / payment / aggregation of the trading fee.


### Details


First, we add a new protocol rule, for valid messages:

    if share-tokens move (within a channel) {
        

        1. Require a counter (Bitcoin's 'sequence numbers') to be incremented.

        // We will explain how this is enforced later.

        // "Cash" is allowed to move, without triggering this rule.

    }

We will use this as a kind of "slope" calculation (change in fees per change in trade-sequence). If the slope calculation is invalid, the honest party will be able to steal the counterpary's funds.

This will be accomplished using two new paths: "Guilt" and "Trial". Guilt is enforced with one of two new opcodes: "Check_Guilt_1_Verify" and "Check_Guilt_2_Verify". Trial "Create_Trial_Verify", "Check_TrialVerdict_Verify", and 


### Notation

Let A and B be two individuals ("Alice" and "Bob") who have a channel together. Let A's signature be "Alpha", and B's signature be "Beta".

Let "F" be a funding transaction, and "T1", "T2", ... "Tn" be mutually-exclusive transactions coming out of F. Finally, let "A1", "A2", ... be the versions of "Ti" which are possessed only by Alice, and let "B1", "B2" be possessed only by Bob.

Here are some examples:

![example1](/images/example1.png)

![example2](/images/example2.png)

Here is an application of this notation to the original lightning network (the simplified, "two person" version which applies most to us).

Rightclick > "view", to enlarge:

![ln-1](/images/lightning-step1.png)

Above: The network is in state "I" in green. From here, it may progress to state "II", off chain. Note that only one line coming out of F can make it into a block...the others will all be rejected as double spends.

Below: Alice and Bob have added state "II", and, more importantly, they have each invalidated state "I". With this invalidation in place, the payment has gone through.


![ln-2](/images/lightning-step2.png)

( LN transaction are different from normal Bitcoin or credit card transactions. Typically, when the "electricity" hits your phone, or the cc-machine, the payment goes through. With LN, the payment doesn't go through until you invalidate your current state. )

With the notation established, let us continue.

The following examples will assume, for simplicity, that Bob is always the one who misbehaves, and Alice is always honest.

### Path 1: Guilt

Most basically, Bob might propose a state update, but *decline* to include the trading fee.

How is Bob punished for this? Alice submits A1 to get her money back, and then:

    guilt( type=1, marketID, marketData, A1, A2, A1_beta, A2_beta )

At which point the computer:

1. Uses "marketID" to link the share transfer to "marketData".
2. Uses "marketData" to extract the trading fee.
3. Uses A1 and A2 to establish "actual fee".
4. Uses A1 and A2, with "marketData", to establish "expected fee".
5. Verifies that "actual fee" and "expected fee" differ from each other.
6. Uses A1_beta and A2_beta to establish that Bob is, in fact, guilty of submitting A1 and A2.

In step 3, guilt can also be established if A1 and A2 have the same sequence number.

Thus, we can be assured that [1] each trade will have a unique sequence number, and [2] for any two consecutive sequence numbers, fees will accumulate correctly.

However, what if traders conspire to select random sequence numbers (71, 604, 80, 9, 301, ...)? We need to guarantee that, as the name implies, these numbers are always chosen in a sequence (1, 2, 3, ...).

### Path 2: Trial

In this case, Bob has failed to comply with sequential sequence numbers. Instead of updating from A2 to **A3**, he is trying to persuade Alice to cheat, by passing her a signed copy of **A4**. He does this because he knows that they can mutually escape the guilt function (described above). Since they can escape the guilt function, they can cheat on paying trading fees.

How is Bob punished for this? Alice submits A1 to get her money back, and then:

    trial( A4, A4_beta, trial_alpha )

Which alleges that transaction-pair (A3, B3) never existed. Specifically, that B3_alpha doesn't exist.

Let us discuss how this accusation establishes Bob's unique guilt. When attacking, A4 is created before (A3, A3_beta, B3, B3_alpha) are created -- otherwise we would be able to use them to establish guilt. The most incriminating evidence against Bob is that is definitely supposed to have B3_alpha at *exactly* this point: [1] Bob has no way of fabricating it, without Alice's private key, and [2] Bob needs to retain B3_alpha (non-invalidated), until *after* Alice sends over B4_alpha.

The computer:

1. Uses A4 and A4_beta to extract public key A.
2. Flips A4 around, to construct canonical B4.
3. Imagines what B4_alpha would look like, and waits for it.

They can't work together to circumvent this system, because one of the two must "move first". If Bob waits for Alice to make a fake B3_alpha, Bob can use Guilt against Alice.

So trial succeeds, after a TimeLock, if Bob cannot produce B3_alpha.


### The Other Guilt

On the other hand, what if Bob decides to use the trial feature to his own nefarious purposes? Perhaps, Bob will constantly accuse Alice of mis-incrementing. Alice has to constantly defend herself against frivolous trials. How can we publish Bob for these frivolous lawsuits?

Bob has just used:

    trial( B4, B4_alpha, trial_beta )

And has just signed a statement alleging that A3_beta does not exist. Alice, of course, has the A3_beta, and can prove her innocence. 

But now she wants revenge. How might we allow her to get some?

Well, Alice submits A3 to get her money back (as always), and then uses:

    guilt( type=2, trial( B4, B4_alpha, trial_beta ), A3_beta )

This proves that Bob asked for a trial, wrongly. As a result, Alice can now steal all of Bobs money.

We now have achieved a new condition: [3] no one will skip sequence numbers when they propose updates.

When combined, these three conditions solve our incentive-compatibility problem.

Below: Beginning to sketch out the normal Bidirectional Channel.

![ln-new-1](/images/lightning-pre-modification.png)

Above: Normal.

Below: With the modifications discussed above.

![ln-new-2](/images/lightning-post-modification.png)


### Not Overdoing It

We'd like to prevent this cumbersome setup from damaging the benefits of the original LN.

To do this, we only force a sequence number to increment if *any share-tokens* are traded. Otherwise, it does not need to increment, thus it is fully compatible with cash transfers on the Bitcoin lightning network. Users can take their Bitcoin, within a payment channel, and ~instantly pay it into a Truthcoin Trading Channel, and proceed to ~instantly make trades with it. Then, they can instantly sell and withdraw back to the Bitcoin mainchain.

This is what allows us to painlessly ban all transaction types that aren't "buy", "sell", "create channel", "close channel", and "rollover channel". All stored value can rest safely in Bitcoin, until it is ready to hop over to Hivemind for use.