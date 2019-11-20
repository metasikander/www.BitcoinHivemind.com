# Capitalizing on Market Manipulation with “Augmentation”
*Paul Sztorc
truthcoin@gmail.com*

## Summary
Prediction Markets (PMs) are highly resistant to manipulation. Firstly, any uninformed trades represent risk-free arbitrage opportunities. Informed traders may actually encourage would-be manipulators to enter a PM, much in the way that professional poker players or pool sharks enjoy taking money from amateurs.  Random (or “noise”) trades, far from harming market accuracy, actually increase the returns to informed trading resulting in a more-informed market price. Finally, all forecasting tools are both aggregators and providers of information, opening up a “self-fulfilling prophecy” manipulation possibility. Forecasts can prevent this manipulation with “augmentation”, and, in Truthcoin PMs, an entrepreneur who “augments” a manipulated market enjoys risk-free arbitrage opportunities.

## Manipulation
Prediction Markets (PMs) are difficult to manipulate, particularly when they are anonymous and competitive. For human-independent outcomes, any attempt to knowingly distort the price[^1] must be done under paranoia: anyone who learns of the scheme (even a fellow schemer) can profit from anonymously un-manipulating. When barriers-to-entry for trading are low, any manipulative algorithmic-trader[^2] will open up profit opportunities for an anti-algorithmic-trader who games the previous algorithm. Even if the manipulator is not un-manipulated by a rival manipulator, his (by-definition uninformed) trading activity increases the returns to informed trading and actually increases market efficiency.[^3]

However, one specific type of manipulation is possible in all forecasting mechanisms (including all markets, prediction or otherwise): the self-fulfilling prophecy. This manipulation exploits the dual-role of a forecast as both aggregator and provider of information. In a PM, traders feed information into markets through their trades, and prices returned from those markets have an influence on consumption and investment decisions. For example, if many believe in a startup, its financing costs may drop and odds of eventual success would therefore increase. Conversely, an unusual idea may never achieve financing at all, and thus never exist (remaining in a permanent state of non-success).

## Augmentation
Truthcoin PMs allow users to create and profit from new markets. This ability can be used in a very specific way (“Augmentation”), which prevents the self-fulfilling manipulation and allows entrepreneurs to profit at the expense of would-be manipulators.

Augmentation is the creation of a new “augmented” market which simultaneously predicts the target outcome and any number of influential intermediate decisions. This allows the public to view conditional prices (“If X occurs, the probability of Y is 40%”), and therefore the likelihood of an event given that these influential intermediate decisions are made a certain way. Traders in a market using a logarithmic market scoring rule (LMSR) can place bets which are uniquely conditional (for example, betting that X given Y is more likely, without directly betting on the likelihood of X in general or Y in general).

TODO: Image from page 3

Figure 1. The flow of information through a Prediction Market, with private individual elements (ovals) contributing to public aggregations (rectangles). All PMs aggregate information in the hopes of providing accurate expectations and better decisions, but some PMs have an ‘endogenous price’ if a market price can influence its own future outcome (red, dashed arrow). This can only happen when the expectations produced by the market price on a given day will affect intermediate (between that day and the outcome) and influential (having an effect on the event) decisions.

## Example: Research and Funding
TODO: Image from page 4

Market 1 (Un-augmented). Suppose that an individual, wishing to prevent the rise of cold fusion, has bet on State 1 (bringing the price up to, say, 80%), knowing that Congress (and others) will deny funding for a project with a low chance of success. When the required research goes unfunded, the technology is never developed, and the manipulator not only prevents the rise of cold fusion, but profits by selling his State 1 shares for 100% each.

TODO: Second image from page 4

Market 2 (Augmented). A ‘protector-entrepreneur’ (PE) may create this Market to attract Traders who are wary of manipulation. Prices of 79%, 1%, 11%, and 9%, (for States 1, 2, 3, and 4) would reveal that, while the pre-funding-decision probability of cold fusion within 5 years is only 20%, if funded, the likelihood is actually 90% (.09/(.01+.09)). Research patrons would then understand the merits of the research, leading to its funding. Before creating this Market, the PE can actually take advantage of Market 1’s incorrect prices. After creating this Market, the PE enjoys the resultant trading fees (Market 2 dominates Market 1 on optionality, stability, and liquidity).

TODO: Table on page 5

Table 1. Other examples of Augmentation. In general, Augmentations will be versions of the manipulable Decision which are more specific and achievable, and occur earlier in time. This is because augmentations must still be probable under a climate of doubt and disunity.

[^1]: By “knowingly distort”, I refer to any trade (purposeful or accidental) which fails to move the market price toward the Trader’s personal expectation of the true likelihood of the relevant outcome.
[^2]: By “manipulative algorithmic-trader”, I refer to a set of trading rules which attempts to generate trading profits without knowledge of the outcome and by instead taking advantage of, for example, market psychology.
[^3]: [http://hanson.gmu.edu/biashelp.pdf](http://hanson.gmu.edu/biashelp.pdf)
