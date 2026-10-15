---
tags:
  - latent
  - books
  - book/softwar
type: chapter
author:
  - Gustavo Grancieiro
description:
aliases:
date created: Thursday, October 15th 2026, 11:46:44 am
date modified: Thursday, October 15th 2026, 11:47:13 am
---

### Chapter 4

- 98% of Fortune 100 companies depend on Oracle software to manage information
- However: they debug in production; nothing is successful except the database; CRM is horrible for post-sale; hyper aggressive marketing belittles rivals, overclaims; consulting arm canibalizes customers; unable to keep executives; Ellison is either detached or excessively dominant.

- Goal: desire to control his environment so he doesn’t work with or for people he didn’t like
- Inconformista, never graduated, programming was quick (short attention spam) and nobody cared about a degree.
	- Dress up, arrive on time, deferential attitude as opposed to how well you do your job.
	- What’s your stance on this?
- Ampex, met partners and CIA-funded project Oracle
- Made VP of R&D, said no bright people found
- Created company with partners to bid for Ornex contract
	- Goal: work less, have freedom

Ellison read IBM’s System R papers on SQL, which built on Ted Codd’s relational theory, and decided to build the first _commercial_ relational database. His reasoning:

- Conventional wisdom said relational databases couldn’t be made fast enough, so nobody else was trying.
- IBM wouldn’t risk its own IMS database business.
- Targeting minicomputers rather than mainframes kept them away from IBM.

He calls it the first of many high-risk decisions he made only when the risk improved Oracle’s odds of winning.

**Early traction.** The CIA was the first customer, followed by the NSA and Navy and Air Force intelligence. Ellison called the first release “Version 2” because he thought no one would buy a version 1 from five guys in California. A late performance breakthrough made it 10x faster. The company nearly ran out of cash because government contracts took six to nine months to pay, and Ellison’s second marriage ended because of his work hours. Venture capitalist Don Lucas noticed the office lights were always on and became chairman.

**Key strategic moves:**

- **Portability.** Version 3 (1983) was rewritten in C so one code base could run on almost any machine. This became central to the sales pitch.
- **Sales.** Board member John Clark taught Ellison that more salespeople meant more sales. The sales force “replicated like a virus” under Mike Seashols, then Gary Kennedy. Early hires included Tom Siebel, Craig Conway and Sohaib Abbasi.
- **Overseas distributors.** Ellison contrasts Europe’s “farming” sales culture with America’s “hunting” one.

**Fending off Ingres.** Ingres, the commercial version of Stonebraker’s Berkeley database, was growing faster than Oracle, and Version 3 had quality problems. Ellison rebuilt engineering with recruits including Derry Kabcenell from Xerox PARC, Andy Mendelsohn and Roger Bamford. This “kernel group” stayed together for decades. Version 4 (1984) added read consistency, and ANSI’s adoption of SQL over Ingres’s QUEL finished Ingres off. Miner was the beloved “shop steward” of the engineers, while Ellison handled hiring and product direction.

**The next threat.** Sybase arrived with a database built for client/server computing, with stored procedures, two-phase commit and referential integrity. Ellison had promised to double revenue every year, so he ordered a full kernel rewrite for Version 6. Under heavy sales pressure, Oracle shipped it in 1988 with far more bugs than anyone expected. That decision began the crisis of the next chapter.

### Chapter 5: To the Limit

In 1985 Ellison promised to double revenue every year, and Oracle did it five years running, from $24M to $916M. It went public in March 1986, one day before Microsoft. Ellison owned 39%. In 1988 he went further with a "Five in Five" plan, $5B in five years, that he later called "absurd and naive."

Behind the growth was what Ellison calls "management by abdication." He ran engineering and ignored the rest. He made Jeff Walker, his head of applications, CFO because Walker was smart. When Kennedy complained legal was slowing deals, Ellison moved legal under sales. Reps then sold software customers wouldn't need for years at huge discounts, sold to customers who couldn't pay, and even proposed bartering software for jets. Sales planned to hire 1,500 reps in nine months. **By 1990, customers owed Oracle $468M on $971M of revenue.**

In March 1990 Oracle wrote off $15M of bad deals and the stock fell 30% in a day. Ellison promised to catch up, and Kennedy delivered one more strong quarter, partly with commissions paid in gold coins, by pulling future sales forward. **The next quarter collapsed.** Oracle posted its first loss, restated three quarters of earnings and was fined by the SEC. The stock fell from $28 to $4.88. **A bank syndicate cut its credit line, and at one point Oracle was within $3M of its overdraft limit.** Tom Siebel left. Ellison faced margin calls on loans against his shares, his marriage ended, and cofounder Miner wanted to sell.

Symonds puts most of the blame on Ellison. He set impossible targets and built a culture of aggression; one ad showed Oracle as a fighter jet shooting down a rival's biplane. He chose a CFO casually and refused to raise cash when the board urged it. The defense is that enterprise software was immature, and that market share really did decide who survived. The chairman kept Ellison as CEO over part of the board's objections. Walker: "If you take a brilliant, compulsive personality and subject them to a learning experience, they learn brilliantly and compulsively."

**Takes**

- **You get the sales culture your targets pay for.** Ellison set "double every year" and was surprised by how Kennedy hit it.
- **Revenue is vanity; receivables are reality.** $468M owed on $971M of revenue isn't growth. It's an interest-free loan to your customers.
- **Discounting next year's demand into this quarter is borrowing at ruinous rates.** The bill came due two quarters later.
- **The crash was an operations failure; the near-death was a financing failure.** Raise money when you don't need it.
- **"Smart" is a trait, not a qualification.** Geoff Squire's question about Walker was the right test: "Yes, he's very smart, but can he do his job?"
- **Counter-take:** the same recklessness may be why Oracle exists today and Ingres, Informix and Sybase don't.

### Chapter 6: Growing Up

Ellison’s recovery plan had three parts: fix the cash problem, bring in experienced managers, and ship a database that beat Sybase.

**1. Cash.** Ron Wohl negotiated with Nippon Steel. Ellison let the talks drag on deliberately, because Oracle’s finances improved every day they waited. The final deal was an $80M loan on good terms, plus warrants for up to 25% of Oracle Japan. Oracle gave up no parent-company equity.

**2. New managers.**

- **Jeff Henley** became CFO in 1991. He was a conventional, steady finance executive. He approved the cleanup Walker had blocked, hired experienced staff instead of young high-flyers, and cut lavish spending. Noosheen Hashemi, who ran finance for U.S. sales, complained that Oracle “became a job, when it had been a mission” and that “people started having children.”
- **Ray Lane**, a consultant from Booz Allen, was hired to run U.S. sales. Ellison tripled his stock options on the spot. Almost everyone Lane asked told him not to join. He set Ellison two tests, and Ellison passed both:
    - Backing Lane’s firings, including Craig Conway, without interfering.
    - Accepting a McKinsey study showing customers hated Oracle and trusted Sybase.
- Lane changed how salespeople were paid. He set quotas by account size, so no one could sell a customer everything at once with a 90% discount, and he refused to pay extra for good service. Many of the “cowboys” left.
- **Robert Shaw**, also from Booz Allen, grew consulting from 200 poorly suited staff to 17,000 people and nearly $3B in revenue. This made Oracle a competitor to the big consulting firms, a deliberate risk because it could push those firms to recommend rivals like SAP and PeopleSoft to clients.

**3. Oracle 7 (1992).** Ellison called it “a working version of Oracle 6 plus a few very important new features.” It matched Sybase’s selling points and did them better: two-phase commit and referential integrity took a few keywords of standard SQL instead of hundreds of lines of code. It also handled distributed queries across servers and won performance benchmarks by wide margins using clusters. One salesman said a “dog with a note in its mouth could sell it.” Nine months after Lane arrived, the stock jumped from $15 to $23 in a day.

**Ellison’s mistakes of 1993.** Ellison gave Lane control of global sales and customer support too quickly. He fired Squire over a London breakfast, which he now calls “the mother of all the management mistakes.” Miner gave up running development after a blow-up over the Oracle 7.1 schedule, and he died of lung cancer about two years later.

**The database wars.** Ellison chose market share over profit. In his words: “I don’t give a shit about profits. I want to beat Sybase.” The top executives’ bonus was tied to market share. Sybase badly missed a quarter in early 1994 and never recovered, and Informix broke about 18 months later.

**Video-on-demand.** Ellison used nCUBE, a parallel-computer maker he owned privately, to build a video server. The technology worked in trials with BT in Ipswich and in the US. It failed for economic reasons: consumers wouldn’t pay enough to justify billions in fiber networks, and cheaper alternatives arrived, including DSL, digital TV and the web. Still, it put Ellison on the cover of _Fortune_ and made Oracle a name known outside IT. Marc Benioff calls this Ellison’s “martial arts of business”: a move that raises Oracle’s profile while unsettling rivals.

By 1994 Oracle had won the database wars. The chapter ends by setting up the next challenge: the applications business, which was supposed to drive future growth, was still struggling.