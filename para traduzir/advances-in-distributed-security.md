Advances in Distributed Security 
Nick Szabo
================================

#### 2003

- [Nick Szabo](#nick-szabo)
      - [2003](#2003)
    - [Introduction](#introduction)
    - [Fault Tolerance and Security in Networks and Their Services](#fault-tolerance-and-security-in-networks-and-their-services)
    - [Partial and Total Orders](#partial-and-total-orders)
      - [Lamport (Causal) Order](#lamport-causal-order)
      - [Breaking Ties – Creating a Fair Total Order](#breaking-ties--creating-a-fair-total-order)
    - [Some Cryptographic Primitives](#some-cryptographic-primitives)
      - [Oblivious Transfer](#oblivious-transfer)
      - [Bit Commitment](#bit-commitment)
      - [Multiparty Secure Computation](#multiparty-secure-computation)
      - [Threshold Cryptography](#threshold-cryptography)
      - [Fair Coin Tosses](#fair-coin-tosses)
      - [Against Traffic Analysis](#against-traffic-analysis)
    - [Physical Broadcasts and Global Clocks](#physical-broadcasts-and-global-clocks)
      - [Canonical Bells](#canonical-bells)
      - [Natural Broadcasts](#natural-broadcasts)
      - [Natural Clocks](#natural-clocks)
      - [Ladies and Gentlemen, Set Your Watches](#ladies-and-gentlemen-set-your-watches)
    - [Secure Time-stamping](#secure-time-stamping)
    - [The Byzantine Generals Problem](#the-byzantine-generals-problem)
    - [Logical Broadcast Over the Internet](#logical-broadcast-over-the-internet)
    - [Byzantine-Resilient Replication](#byzantine-resilient-replication)
    - [Some Applications](#some-applications)
    - [Conclusion](#conclusion)
    - [Appendex A – Implementations](#appendex-a--implementations)
      - [Byzantine-Resilient Replication](#byzantine-resilient-replication-1)
      - [Traffic Analysis Reistant Messaging](#traffic-analysis-reistant-messaging)
      - [Blind Signatures and Bearer Instruments](#blind-signatures-and-bearer-instruments)
      - [Hash Chain Structures and Secure Time-stamping](#hash-chain-structures-and-secure-time-stamping)
      - [Oblivious Transfer and Multiparty Secure Computation](#oblivious-transfer-and-multiparty-secure-computation)
      - [Capabilities / Smart Sandboxes](#capabilities--smart-sandboxes)
    - [References](#references)

### Introduction

The last decade has witnessed a revolution in distributed security. Old, pessimistic proofs that security and fault tolerance were "impossible", based on assumptions that protocols had to be deterministic and security and fault tolerance properties had to be absolutely certain, have given way to new proofs and implementations of provable security based on the assumption of cryptography and other randomized protocols that achieving security with very high probability is sufficient. The old view "proved" that the integrity properties of a wide variety of services on which civilization depends, whether [synchronized clocks](http://szabo.best.vwh.net/synch.html), [public directories]({{url_for('slugview',%20slug='secure-property-titles')}}), [censorship-proof file sharing and publication](http://oceanstore.cs.berkeley.edu/), or [issuing money or securities]({{url_for('slugview',%20slug='contracts-with-bearer')}}) were "impossible" on asynchronous networks like the Internet unless we put unlimited faith in a third party to enforce many of the rules of the service. We now know how to provide such services with a high degree of integrity and availability, yet far more resilient to the possibility that any party might act in a malicious manner.

### Fault Tolerance and Security in Networks and Their Services

As a result of these new possibilities, we are witnessing a shift in the way we view trust. The old view in computer and network security was that trust was all-or-nothing – either we must place an essentially blind faith in a third party (for example a certificate authority or an issuer of digital cash) or we must protect against a particular mode of attack completely (as, for example, encryption protects against wiretappers). The old view could not handle most real-life situations which don't fall into either of these extremes. Among knowledgeable distributed security designers, unconditionally trusted third parties are now viewed as a cheat – "here we pray for heavenly benevolence", analogous to the comic-strip mathematician whose proof contains the crucial step, "here a miracle occurs". A third party fully trusted with a security property means that property in fact remains fully insecure – it means the protocol designer has fobbed off security on somebody else rather than actually solved a security problem.

The new view reiterates the desirability of complete protection against attack where it is available, but it adds protection against vast new classes of attacks, and protection of a wide variety of other desirable properties of distributed system, that are impossible to protect without at least some trust assumptions. The new trust assumptions are that participants in a critical public service are partially, usually, or more often than not trustworthy, and often only under certain conditions. The set of parties that make up a critical distributed service is never either completely trustworthy nor all malicious.

Modern protocols for critical services such as public directories construct, out of all possible subsets of all participants, *attack structures* consisting of the worst combination of malicious parties that be tolerated, and their complement, *access structures*, the minimal set of parties that need to act correctly during this operation to perform the function. (Note that access structures have nothing to do with access control lists, a traditional security method that assumes a fully trusted third party and consists of a static list of persons or classes of persons and the resources or classes of resources they have access to).

One particular simple example of such an attack and access structure is a *threshold* structure where the malicious behavior of up to t out of n participants can be tolerated. Although we will describe the protocols below in terms of threshold structures, it will usually be possible to substitute other partitions of the power set of participants into minimum access and maximum attack structures.

A given property of a system has *perfect security* if its access structure is any participant and its attack structure is the empty set. An example of a property with perfect security is the use of a spinning neutron star called a *pulsar* as a clock. Its access structure is any party that can receive its natural broadcasts, and its attack structure is the empty set – given the reasonable presumption that there are no aliens out there who can and want to manipulate the very high energy outputs of pulsars in pursuit of some human ends they have learned about.

Another perfect security property is that of encryption against third parties, assuming the encryption is unbreakable. However, if we take into account the receiver of a message as a possible attacker, the broader privacy property is not secure – the receiver is an attack structure of one who can compromise privacy of the entire message encrypted to him.

A security property is *almost perfect* if its attack structure must contain T-1 out of N participants. For example, in the *digital mix* of Chaum<sup>[[C81]](#fnC81)</sup>, for a single message, it would take collusion of N-1 out of N of the mix servers to trace a message. The untraceability property of this system has almost perfect security for a single message. On the other hand, the reliability property of the digital mix is almost perfectly insecure, since any one of the n mix servers can block a message from getting through. Often we must trade off two different properties like this. Since reliability is an error reversible by the end user and a privacy breach is not, the tradeoff made here by Chaum makes sense.

Alas, for many desirable properties we cannot achieve either perfect or almost perfect security. For some properties of replicated services – for some kinds of rules they advertise as following – we can achieve almost perfect security through, for example, the use of cryptography.

For any other properties, the maximum attack structure of malicious and colluding servers that can be tolerated is the set complement of the access structure. For the threshold case, this means that T, the maximum number of malicious and colluding servers that can be tolerated, is a certain fraction of the total number of servers, such as 1/3 or 1/2, of the total number of servers comprising the service, N. That is to say, if T+1 out of N of the servers jointly decide to violate the service's rules and thereby corrupt the system, they can do so. Those who wish to stick to the rules must back out of the corrupted transaction and restart the service out-of-band. For this large class of service properties where the access structure is the set complement of the attack structure, the security of a property is neither perfect or almost perfect at one extreme, nor fully depends on a single trusted party at the other extreme. We say that this class of service properties can be implemented with *distributed* security.

Three of the properties we most often want to protect are privacy, liveness (a.k.a. availability) and integrity. For a replicated service, the main focus of this article, we focus on the security of the integrity and liveness of a single operation of a service. The goal is to create attack structures that are very highly unlikely to fail. If or when such failures of widespread collusion do occur, *relying parties*, i.e. parties who depend on the properties being secured, must go "out-of-band" and use supplementary systems to repair the system. These supplementary systems might include a wide variety of interparty integrity constraints, audits, blacklisting, and other schemes involving auditing, reputation, and/or cryptography by participants, relying parties, or third parties. These can further motivate servers to preserve the integrity and liveness of these services, and help users to recover after a (now much rarer) successful attack.

Since a wide variety of trust assumptions can now be made by a security protocol and this variety can for the first time be described mathematically – as attack and access structures – these supplementary systems can focus on keeping the actual attack structures smaller than the maximally tolerated attack structure, rather than on vastly more difficult task of plugging wide-open security holes called "trusted third parties" with these more loosely defined or traditional supplementary institutions.

### Partial and Total Orders

A basic issue of security and fault tolerance that must be resolved is the secure determination of which order events occured in. If a contract specifies a deadline and it goes down to the wire, how can a relying party or third party adjudicator determine whether the deadline was met? The outcome itself, and its fairness, may rest on fairly deciding who came first. If Alice tries to double-spend a piece of digital cash<sup>[[C82]](#fnC82)</sup>, only the recipient who checks with the bank first is entitled to its value. But if the bank servers are replicated, which of the two recipients Bob or Charles checked with the bank first? In the case of a [replicated property title service]({{url_for('slugview',%20slug='secure-property-titles')}})<sup>[[S98]](#fnS98)</sup> we have a similar problem – if Alice transfers her title to two other owners, which new owner actually received the deed? If property is homesteaded on a first-come first-serve basis, which of two or more "land rushers" competing for a lucrative parcel is entitled to the land?

#### Lamport (Causal) Order

Imagine a network where computers don't know how to keep time very well – they are always getting out of synchronization. (Alas, all you have to really think of here is the actual Internet with PCs). Such a network, called an *asynchronous* network, lacks an accurate and secure global clock time by which computers can determine the order in which events, which might be messages sent or instructions executed on a particular local machine, have happened. Lamport<sup>[[L78]](#fnL78)</sup> was among the first to tackle the problem of how to determine the order of events in such a network.

A partial order means that we know in what order some of the elements are, but we aren't sure about some of the others, or some of the others may be equal. An example is the "less than or equal to" relationship among a group of integers, some of which can repeat. Some of the integers we know are less than some others, but an integer paired with itself is equal. A total order, on the other hand, is like the "less than" relationship among unique integers – we can always tell when one integer is less than another – there is no ambiguity left. In the case of events, a partial order means for some pairs of events we know whether one occured before another, and for some others we don't know. We use the same symbols as we would use for the analogous case of the integers, so that "x \<= y" means "x either occured before y or we don't know whether it occured before or after y". In a total of events, we know for any two events which one happened first. We write "x \< y" meaning "x occured before y."

Lamport's answer to the event ordering problem was to show that parties (or, we use the terms equivalently here, nodes on the network) can agree on a partial order of events based on causal relationships between these events – or at least the subset of events where we can determine that causation could occur. On a network, parties influence each other by talking to each other – in other words, by sending each other messages. Lamport used these messages as the basic building block for constructing his partial order, according to the following rules:

1.  If an event is local to node P, every nonfaulty node agrees on P's opinion of it.
2.  Every correct node agrees that every message was sent before it was received.
3.  If we agree that event A occured before event B and that event B occured before event C, then we agree that event A occured before event C. In other words, this partial order is transitive.

#### Breaking Ties – Creating a Fair Total Order

The partial order leaves us with the need to agree on how to break ties – how to resolve the ambiguities where we can't agree which event took place first – and thus create a total order of events. We want to do so in a way that is *fair*, in other words, in a way that cannot be manipulated to the advantage of any particular party.

An unfair way to create a total order would be to impose a certain predictable rule for breaking ties. For example, we could decide on a total order for the processes and break ties in the causal order by referring to this total order.

However, such a procedure creates a bias that may, depending on the application, favor certain servers over others, and therefore allow those servers to favor certain clients over others.

One way to break ties fairly is have the participants toss fair coins – in other words, generate random numbers in a way that cannot be manipulated and then assign those random numbers to events. There are several ways to toss fair coins over a network and we describe one such way below.

Another way to break ties fairly is to have the participants agree to a global clock time that is more accurate than the message delays faced by those who would manipulate timing in favor of some party. This entails using a network with very predictable message lag for the clock synchronization protocol and a less predictable one for the other services. We will describe how to do this below.

### Some Cryptographic Primitives

Certain cryptographic primitives play a crucial role in the recent breakthroughs in distributed security that we will discuss here.

#### Oblivious Transfer

Oblivious transfer is an important building block of multiparty secure computations and related protocols. Rather than describing it here, we recommend [this](http://www.argreenhouse.com/papers/rafail/book.ps) good introduction.

#### Bit Commitment

Alice wants to prove that she can predict the stock market. But she doesn't want to actually reveal her choice to Bob or anybody else until she's actually had a chance to trade on her prediction. But after the fact, she could just read the closing price and pretend to Bob that she predicted it. How can Alice prove to Bob that she actually predicted the market? Using bit commitments.

Bit commitments are ways to commit to a string of numbers or data, in such a way that if or when one later publishes the data, it cannot be forged – it must be the same as the data you earlier committed to.

Alice can commit to her data using one-way functions – functions that are much harder to compute one way than another. (One-way functions are the most basic building block of cryptography). A common kind of a one-way function is a cryptographic hash function.

To create a bit commitment, Alice first generates two random numbers. Then she computes the bit commitment by hashing the two random numbers and the data to be committed to. Append on of the random numbers to the end of the hash and sends it to Bob. The next day when Bob wants to examine the data, and prove that it matches the data Alice originally committed to, Alice provides the data along with the second random number. Bob can verify that it is astronomically unlikely that Alice was able to commit to one predication and then later tell Bob she predicted something else.

This protocol is called "bit commitment" because one can commit to even an individual bit this way. If the data has enough entropy one can commit to that data simply by using a hash function and dispense with the random numbers. We will see below how with secure timestamping other parties can determine when the data was committed to.

#### Multiparty Secure Computation

The ideal protocol would have most trustworthy third party imaginable – a diety who is on everybody's side. All the parties would send their inputs to God. God would reliably determine the results and return the outputs. God being the ultimate in confessional discretion, no party would learn anything more about the other parties' inputs than they could learn from their own inputs and the output.

Network security theorists have recently solved this problem to an astonishing extent. They have developed protocols which create virtual machines between two or more parties. Multiparty secure computation allows any number of parties to share a computation, each learning only what can be inferred from their own inputs and the output of the computation. These virtual machines have the exciting property that each party's input is strongly confidential from the other parties. The program and the output are shared by the parties.

For example, we could run a spreadsheet across the Internet on this virtual computer. We would agree on a set of formulas and set up the virtual computer with these formulas. Each participant would have their own input cells, which remain blank on the other participants' computers. The participants share output cell(s). Each input our own private data into our input cells. Alice could only learn only as much about the other participants' input cells as she could infer from her own inputs and the output cells.

More information on this exciting breakthrough can be found in the accompanying article ["The God Protocols"]({{url_for('slugview',%20slug='the-god-protocols')}}). Often, as in the spreadsheet example above, the resulting protocol would be very slow. We will now discuss a special efficient kind of multiparty secure computation – *threshold cryptography*.

#### Threshold Cryptography

Threshold cryptography has been used to help achieve Byzantine-resilient replication in Rampart, Fleet, SITRA, and several other distributed service or filesystem architectures. Threshold cryptography is an optimized special case of a more general technique called multiparty secure computation

In a *threshold public-key cryptosystem* there is a single key for encryption, but each party holds a *key share* for decryption. A threshold scheme implements the threshold case of distributed security as described above. Any T+1 key share holders are needed to jointly perform a decryption, and any N-T key share holders can collude to prevent a decryption from being performed. The parameter T can be set at any positive integer between 1 and N. Often a more general access structure, under the distributed security constraint that the access structure is the set complement of the attack structure, can be implemented as well.

For some algorithms one must assume a trusted dealer to generate a private key and distribute shares; for some other algorithms a mutually confidential generation of key shares is possible. During the decryption protocol, each party processes a decryption request for a particular ciphertext and output a decryption share together with a proof of its validity. When a party obtains the ciphertext and at least T+1 valid encryption shares, it can recover the message. In the case of threshold signatures, when at least T+1 signature shares have been obtained, a valid signature can be constructed. [C01]

#### Fair Coin Tosses

Joe Killian introduces this problem as follows<sup>[[K90]](#fnK90)</sup>:

> Alice and Bob wanted to flip a fair coin, but had no physical coin to flip. Alice offered a simple way of flipping a fair coin mentally.
>
> First, you think up a random bit, then I'll think up a random bit. We'll then exclusive-or the two bits together," she suggested.
>
> "But what if one of us doesn't flip a coin at random?" Bob asked.
>
> "It doesn't matter. As long as one of the bits is truly random, the exclusive-or of the bits should be truly random," Alice replied, and after a moment's reflection, Bob agreed.
>
> A short while later, Alice and Bob happened upon a book on artificial intelligence, lying abandoned by the roadside. A good citizen, Alice said, "One of us must pick up this book and find a suitable waste receptacle." Bob agreed, and suggested they use their coin-flipping protocol to determine who would have to throw the book away.
>
> If the final bit is a 0, then you will pick the book up, and if it is a 1, then I will," said Alice. "What is your bit?"
>
> Bob replied, "1."
>
> "Why, so is mine," Alice said slyly. "I guess this isn't your lucky day."

Bruce Schneier<sup>[[Sh96]](#fnSh96)</sup> goes on to describe what is wrong with this protocol:

> Needless to say, this coin-flipping protocol has a serious bug. While it is true that a truly random bit, x, exclusive-ORed with any independently distributed bit, y, will yield a truly random bit, Alice's protocol did not ensure that the two bits were distributed independently. In fact, it is not hard to verify that no mental protocol can allow can allow two infinitely powerful parties to flip a fair coin. Alice and Bob were in trouble until they received a letter from an obscure graduate student in cryptography. The information in the letter ws too theoretical to be of any earthly use to anyone, but the envelope the letter came in was extremely handy.
>
> The next time Alice and Bob wished to flip a coin, they played a modified version of the original protocol. First, Bob decided on a bit, but instead of announcing it immediately, he wrote it down on a piece of paper and placed the paper in the envelope. Next, Alice announced her bit. Finally, Alice and Bob took Bob's bit out of the envelope and computed the random bit. This bit was indeed truly random whenever at least one of them played honestly. Alice and Bob had a working protocol, the cryptographer's dream of social irrelevance was fulfilled, and they all lived happily ever after.

On a computer, those "envelopes" are committed bits – see the protocol for bit commitment above. Also see Manuel Blum's landmark paper "Coin Flipping By Telephone"<sup>[[B82]](#fnB82)</sup> for more details. He subtitled the paper "A Protocol for Solving Impossible Problems", which was more prescient than he knew.

Fair coin tosses can be used to create a fair total order of events out of a partial order of events, defined by sending and receiving times for messages, in an asynchronous distributed system. They can similarly be used to achieve atomic broadcast, and thus Byzantine agreement and replication<sup>[[C01]](#fnC01)[[CP02]](#fnCP02)</sup>.

The *threshold coin-tossing* system developed by Cachin, Kursawe, and Shoup [C01] solves the fair coin tossing problem by implmenting a cryptographic pseudorandom number generator (PRNG) is a distributed manner using threshold cryptography. They use their protocol to solve the Byzantine generals problem for asynchronous networks. We will describe the Byzantine generals problem and its solution on asynchronous networks further below.

#### Against Traffic Analysis

There are a wide variety of other cryptographic primitives and protocols, beyond the well-known symmetric and asymmetric cryptosystems, that give us security properties not otherwise in distributed systems, including and mixing and channel padding<sup>[[C81]](#fnC81)</sup> and blind signatures<sup>[[C82]](#fnC82)</sup> to combat traffice analysis.

### Physical Broadcasts and Global Clocks

#### Canonical Bells

In our time, the tallest and most expensive buildings belong to some of our most important economic institutions – multinational corporations. The size and expense of our skyscrapers will provide future archaeologists an important clue that these institutions played a big role in our economy. In the high and late Middle Ages, the tallest structures in Europe were bell towers – larger and more numerous in that region than on any other continent. Chartres in the year 1169 boasted a 437 foot tower, the world’s tallest. These towers, besides the churches they were built upon, were also the most expensive structures in town.

Some historians claim that the size and expense of Europe’s steeples and public clocks, like the size and expense of the churches they were built upon, reflected the predominant role of religion in medieval life, as opposed to business in ours. Given that the churches and cathedrals themselves were expensive, this is a plausible claim. However, the Church also played a leading role in the economy, both by its own economic activities and by its role in commercial law. The church bells and their clocks also played a major economic role.

Telling time was not the only, and perhaps not even initially the main, function of church towers and their bells. An important early function of the bell tower was as an alarm, to inform the town of emergencies such as a fire or attacking army. The towers also sometimes made a good vantage point to detect such events. They tolled for events such as baptisms and funerals. Timekeeping became its primary function, first in order to call people to mass, but soon as a general service the Church provided to the surrounding Catholic community that supported it. Long before the mechanical clock, residents within a few miles of a church started working their schedules around the canonical hours – sundial-based unequal hours – tolled on its bells. Thus in many European cities, long before the invention of the mechanical clock, the local church was trusted to ring the hours. Churches, funded mainly by the nearby parishioners, but often also by the city or directly by a guild of merchants, lavished enormous resources to build, operate, and maintain the towers as well as the bells, and later for the clocks that were installed in those towers. The productive synchronization of human relationships funded the bell towers; the bell towers would provide a ready market for public clocks. Thus did in Europe emerge a "virtuous circle" that would advance both its timekeeping technologies and time-dependent institutions beyond those of the other continents.

The time rung on the bells was mainly read from a sundial. By the 11th century these were often supplemented by water clocks. By the end of the 14th century most were using the new mechanical clock, backed up by another new technology of that century, the more reliable and personally secure sandglass.

In the larger and more important belfries were present at least two bell-ringers. They lived up there full-time<sup>[[D96]](#fnD96)</sup>. This arrangement is an example of the pattern of dual control – each ringer served as a check for the other; neither could spoof the time or other bell signals without the collusion of both.

The heaviest and most expensive elements of the towers were the bells. Bells smiths competed to produce the most distantly hearable ringing. The "Maria Angola" bell, cast in 1659 and installed in a cathedral in Cusco, Peru could be heard up to 25 miles away<sup>[[G95]](#fnG95)</sup>. In Cordova in the 16th century, a cathedral boasted a one-ton bell that could be heard 8 miles away. At the cathedral at Rouen, in 1321, a carillon was installed that played on an array of bells a hymn audible 5 miles away<sup>[[D96]](#fnD96)</sup>. The typical range of a parish church’s bells was 3-5 miles. These bells would primarily be heard and in the surrounding town; larger bells could also be heard by peasants working in the fields miles away.

The most valuable property of the bell tower time was not its accuracy, but its fairness. Even if it broadcast the wrong time, it broadcast the same wrong time to everybody. An employer, even if he was colluding with the Church to bias the sometimes subjective ringing of the canonical hours, couldn’t tell his favorite employees that it was time to go home, while making other employees work extra, and pretend that it was the same time. (In contrast, on our computer networks such "Byzantine" attacks are possible, without advanced safeguards, when "broadcasting" time or other information).

While nearby churches or monasteries provided the public, standard time, workers and employers both often employed their own timekeeping devices as a check. Peasants could tell the time by observing their own shadow against some standard sized object. In Germany and Flanders, even the smallest peasant villages had "quadrants to indicate the hours without the sun". Miners, working underground, followed work bells, operated by the employers, and passed their signal on through the tunnels by workers banging on tools. As a check, the miners had their own marked tallow candles<sup>[[D96]](#fnD96)</sup>. Despite the public broadcast of authoritative time, few dispensed with the option to check their own independent sources.

See the accompanying article ["On Time"](http://szabo.best.vwh.net/synch.html) for more of the fascinating history of Europe's development of clocks and accompanying economic institutions.

#### Natural Broadcasts

Broadcasts using sound or radiation, from sources such as bell towers, radio towers, satellites, and pulsars, must send out the same value to every receiver. A remote beacon such as a pulsar has perfect security: the access structure is any party, and its complement, the attack structure, is the empty set. For human controlled broadcasts, the attack structure consists only of the broadcaster and the access structure is any receiver.

Natural broadcasts are thus immune to the problem, described in the discussion of the Byzantine Generals problem below, of a transmitter sending different values to different receivers. Indeed, as we will see below, distributed researchers have gone to great lengths just to recreate this simple property on the Internet with *logical broadcast* protocols.

#### Natural Clocks

Nature provides clocks that are oblivious to the malicious intentions of any outside parties. In the case of a remote high-energy system such as a pulsar, this means anybody. and many orders of magnitude more accurate than random delays that face attackers on the Internet. If critical Internet servers were synchronized to natural clocks in a secure and timely fashion, they would be immune to attacks that relied on uncertainties in timing. Here are some [comparisons of the stability (error creep)](http://scholar.lib.vt.edu/theses/available/etd-112516142975720/unrestricted/ch4.pdf) in good natural clocks:

||1 sec|1 day|1 month|
|:--|:----|:----|:------|
|Quartz|10<sup>-12</sup>|10<sup>-9</sup>|10<sup>-8</sup>|
|Rubidium|10<sup>-11</sup>|10<sup>-12</sup>|10<sup>-11</sup>|
|Cesium Beam|10<sup>-10</sup>|10<sup>-13</sup>|10<sup>-13</sup>|
|Hydrogen Maser|10<sup>-13</sup>|10<sup>-14</sup>|10<sup>-13</sup>|
|Pulsar|10<sup>-11</sup>|10<sup>-12</sup>|10<sup>-13</sup>|
|Io orbit||||

Pulsars overtake atomic clocks in accuracy after about 4 months.

#### Ladies and Gentlemen, Set Your Watches

The Internet with its wide and unpredictable variances in message delays makes for an extremely poor method of distributing time. Some clock synchronization protocols for an asynchronous network are described in <sup>[[C??]](#fnC--)[[CF94]](#fnCF94)</sup>. Unfortunately, their accuracy is limited to the same order of magnitude of uncertainty as that would face an attacker. So they don't clearly eliminate the possibility that an attacker could take advantage of the different servers hosting a critical service disagreeing on the time.

Far more accurate are the distribution methods, especially radio broadcast, described in this [excellent survey of timekeeping techniques](http://www.educatorscorner.com/tools/lectures/appnotes/discipline/pdf/5965-7984E.pdf).

This article also contains an excellent discussion of the highly distributed system used for reaching agreement on the global standard UTC time. Over 200 centers use their own atomic clocks to update UTC time. This recalibration uses a sophisticated averaging formula that throws out extreme values. There are also 50 centers in 30 different countries that can be queried at any time during the month for the current recalibration according to their own atomic clocks. In addition, there are a variety of services that broadcast UTC time, with varying levels of delay uncertainty and cost that the article describes in detail. The security and tolerance to extreme faults of the entire system from atomic clock to delivery of time updates to relying parties is not clear but probably high. The jurisdictional diversity of the atomic clock sources is far higher than that of common delivery systems such as GPS, but the results of the latter can after the fact be easily checked against the former, keeping the latter honest, so that the resulting end-to-end system is almost universally trusted (taking into account certain well-known adjustments such as selective availability in GPS).

### Secure Time-stamping

[Secure time-stamping](http://kodu.ut.ee/~lipmaa/crypto/link/timestamping/) is a way for a party with a confidential document, or two or more parties sending private messages, to commit to each other and third parties an unforgeable, non-repudiable time-stamp. This time-stamp consists of a place in a total order consisting of this message, other parties' messages, and clock ticks. This commitment is accomplished without the parties having to reveal the actual contents of those messages, unless or until challenged for proof, to any third parties. (Even then, there exist zero-knowledge proofs that allow the party to prove he has a document corresponding to the time-stamp without revealing the document).

These protocols work by users sending a cryptographic hash (a.k.a. message digest) of their document to the time-tstamping servers. The servers chain messages and click ticks together by order of arrival. Replicated servers can break ambiguities in order of arrival with a protocol such as fair coin tossing to achieve a fair total order.

### The Byzantine Generals Problem

Lamport created a theoretical structure for security and fault tolerance in a distributed service with the Byzantine generals problem. These generals might be loyal, following orders and passing them on faithfully, or they may be traitors. The worst-case behavior of traitorous generals is modelled by the nasty trick of sending out contradictory orders – for example, telling one general that the order is to march and another general that the order is to retreat.

(Lamport just meant the Byzantine generals story as an interesting, cartoonish illustration of the theory of fault tolerance against corruption by malicious adverseries, but this kind of problem has actually sometimes occurred among generals. The actual generals of the Byzantine Empire were no more prone to such treachery than any of their enemies, such as the Persians or Turks. If one is partial towards the Byzantines, one can think instead of the Iraqi generals in the current war there – the Coalition generals hope that some of the Iraqi generals will defect and are trying to insert forged messages into their communications network. They hope some generals will be duped into following these specious orders).

There are N generals; one of them is the commanding general or field marshall. They can send and receive messages between each other. The Byzantine generals problem is to develop a protocol for the commanding general to send messages to his N-1 subordinates so that

1.  All loyal generals obey the same order, and
2.  If the field marshall is loyal, every loyal general obeys the orders he sends.

The protocol should be able to resist up to T traitorous generals. In the case of a fully deterministic protocol (no random choices or cryptography allowed) the best we can do is tolerate T = floor(N/3) - 1 generals for a synchronous network. For an asynchronous and deterministic network no traitors at all can be tolerated.<sup>[[FLP85]](#fnFLP85)</sup>

However, the Byzantine general's problem is easily solved by unjammable physical broadcast. Not coincidentally, solving the logical broadcast problem on network where physical broadcast is absent is very similar to, and as hard as, solving the Byzantine generals problem.

The above pessimistic results regarding T on deterministic networks – and the inefficiency of protocols that could provide these weak solutions to the Byzantine generals problem – until recently has discouraged researchers and engineers from finding practical solutions to securing distributed services. However, under only slightly weaker assumptions – those of cryptography, that we need only achieve security with a very high probability – agreement between the Byzantine generals has not only been achieved [Ben-Or] but achieved efficiently [Cachin]. The basic insight in these solutions is that we can break ties in a Lamport partial order in a an unbiased way with random numbers.

### Logical Broadcast Over the Internet

Point-to-point communications is sufficient for many applications. For many others, nodes need to send a message to many other nodes, or *multicast*. We call the simple case where a node sends messages to all other nodes participating in a system *broadcast*.

As we've seen, broadcast can be implemented directly in physical media such as sound and radio. We will discuss the problem of implementing logical broadcast over an asynchronous network that directly supports only point-to-point communications. Such broadcasting protocols are subject to node and communications failures, including malicious attacks.

Four important design criteria of such a logical network are *reliability*, *consistent ordering*, *causality preservation*, and *fairness*. *Reliability* means that a message once broadcast be received by all the functional nodes. *Consistent ordering* means that different messages sent by different nodes are delivered to all the nodes in the same order. *Causality* is preserved if this order is consistent with with the causal order in which messages were sent and received. *Fairness* means that no node can breach the rules or properties of the system we want to protect, particular to some parties advantage or disadvantage, by manipulating this order.

Note that physical broadcasts, if they cannot be jammed, easily have these properties. Since the broadcast medium has a finite velocity, messages might not all be received in the same order as sent. However, the receiving nodes can deduce from the physical properties of the medium the expected time lag at their distance and thereby deduce sending times. We say in this case that messages are *received* in a certain order, queued, and then *delivered* in a possibly different order.

The basic issue here is message delays – some servers receive messages in different order from others. Clock synchronization can reduce the scope of this problem – even eliminate it if done over a network where unpredictability in message lag times are much less than in the network over which we run the other services we wish to secure. In such cases clocks can be synchronized with sufficient accuracy that global clock time cannot be spoofed to reorder messages with significant probability. Where we choose not to implement such a global clock (because, for example, the price of retrofitting services with a radio time synchronization service as described above), we have another option for creating a fair total order – the fair coin flipping methods described above. The result is a logical broadcast with the same basic security properties as an unjammable physical broadcast.

### Byzantine-Resilient Replication

The theory of the Byzantine generals has a practical equivalent – the problem of replicating a serivce – or, equivalently, a distributed object – in such as way as to provide distributed security, or fault tolerance against arbitrary behavior of up to T malicious and colluding servers.

These services or distributed objects are sometimes called "intrusion tolerant", because the replicated service can resist attack and corruption of up to T servers. However, in the real world more perpetrated by insiders rather than intruders. Byzantine-resilient replication of a service across administrative domains or jurisdictions solves both problems.

Several Byzantine-resilient replicated service infrastructures have been implemented . They use techniques such as threshold cryptography and fair coin tossing to achieve logical broadcast on asynchronous networks like the Internet, protected against attack structures of colluding and malicious servers, such that the attack structure is the set complement of the access structure. See Appendix A below for sources of more information. A wide variety of Byzantine-resilient services can be built on top of logical broadcast. A high bandwidth, many-to-many unjammable physical broadcast network might provide similar but more efficient solutions in the future. A Byzantine-resilient replicated object library, for implementing online services with distributed trust in the CORBA distributed object system is described in [this presentation](http://www.omg.org/news/meetings/workshops/presentations/docsec_2001_present/4-1%20Whitmore%20DOCSec%2001-03-28%20Annapolis-ebdg.pdf) and [this paper](http://www.nai.com/common/media/nai/pdf/dsn-itdos-w-ieee.pdf).

The basic system has the ability to replicate stateful objects resilient to up to 1/3 Byzantine (arbitrarily malicious) failures.

In other words, object replication is used to distribute trust in the integrity of data and computations. Instead of obtaining a critical service from a single trusted server – which may be innately malicious or may get cracked by an outsider – one obtains the service from N different servers, and the service maintains its integrity as long as less than N/3 of the Vats are malicious.

Note that the "voting" implicit in Byzantine resilient protocols like that used here protects the integrity of a particular remote method call. Between such invocations, clients can update their own blacklists of servers they have found to be unreliable. With such a blacklist the attacker must manifest their faulty behavior in over N/3 servers during the same call in order to corrupt the call. Once this is discovered the client can blacklist them, removing them from the list of trusted Vats for subsequent calls.

Integrity techniques such as cryptographic hashes, digital signatures, secret sharing, and threshold cryptography can be layered on top of this basic Byzantine-resilient replication system to further increase the integrity of certain properties of the replicated state. Which of these techniques are used, and how, depends on what the critical functionality is that one is protecting.

Replication of course does not distribute trust in the privacy of the data – quite the opposite, it magnifies the exposure. However, where this problem is relevant it can easily be overcome with encryption and/or multiparty secure computation, described above.

A necessary part of any good distributed security toolkit is a diverse cryptographic library, implementing not only symmetric and assymetric primitives but also those described or referred to in this article.

### Some Applications

A wide variety of other applications once thought "impossible" to secure can now be implemented securely.

On a public network a wide variety of values must be agreed upon across trust boundaries, such as mappings of names or addresses to keys (as in a public key infrastructure) or of names to addresses (as in the Domain Name System). Such agreements across trust boundaries can best be thought of as simple kinds of private property to be controlled by their owner, within constrains enforced by the rules followed by the replicated service, a public property titles system.

Whether thought of as property rights or not, a wide variety of such currently centralized services can be re-implemented with much greater ensurable integrity and availability by distributing their trust with techniques such as Byzantine-resilient replication.

Another large class of potential services that can be distributed are issuers of [digital bearer instruments]({{url_for('slugview',%20slug='contracts-with-bearer')}}), such as digital cash.

This author's design for a [secure property title service]({{url_for('slugview',%20slug='secure-property-titles')}}) uses cryptographic hash functions and digital signatures (without the need for a PKI) on top of a Byzantine-resilient replicated object service to maintain the integrity of chains of property titles. It's also suitable for property-like directories such as the Internet's Domain Name System (DNS).

### Conclusion

The old pessimism has been overturned. Old proofs of "impossibility", based on strict insistence in perfect certainty, have given way to new proofs demonstrating how to do the "impossible" by being satisfied with extremely high probability against a sophisticated but computationally bounded opponent – the assumption of cryptography – rather than of absolute certainty. This overturning of the old view has led to a raft of new possibilities for securing distributed applications. The simple protocol of the bell tower, which broadcast to every resident of a medieval town the same time, can now be implemented on a network – either through logical broadcast on the Internet or physical broadcast with radio. For the first time we can implement on the Internet the integrity properties on which civilization depends – including synchronized clocks, unforgeable transactions, and censorship-proof publishing. Where today's Internet, lacking this technology, fails to provide many of these properties, we now know how to provide them with a greater degree of integrity and availability than either the Internet or any previous media was capable of.

### Appendex A – Implementations

#### Byzantine-Resilient Replication

-   [IBM Zurich: SINTRA and MAFTIA – distributing trust on the Internet](http://www.zurich.ibm.com/security/dti/index.html)
-   [ITTC Project (Intrusion Detection via Threshold Cryptography)](http://theory.stanford.edu/~dabo/ITTC/)
-   [OceanStore distributed filesystem](http://oceanstore.cs.berkeley.edu/)
-   [Object replication in CORBA](http://www.nai.com/common/media/nai/pdf/dsn-itdos-w-ieee.pdf)
-   Rampart
-   Fleet
-   [SecureRing](https://web.archive.org/web/20030824133825/http://beta.ece.ucsb.edu/smp/project_sr.html)

#### Traffic Analysis Reistant Messaging

-   [MixMaster](http://sourceforge.net/projects/mixmaster/)
-   [MixMinion](http://www.mixminion.net/)
-   [Onion Routing](http://www.onion-router.net/)

#### Blind Signatures and Bearer Instruments

-   [Lucre: based on Wagner's patent-free variant of Chaumian blinding](http://anoncvs.aldigital.co.uk/lucre/)
-   [Lucrative (bearer instruments in SOAP and based on lucre)](http://lucrative.thirdhost.com/index.php)

#### Hash Chain Structures and Secure Time-stamping

-   [THEX (Merkle hash trees)](http://open-content.net/specs/draft-jchapweske-thex-02.html)
-   [Helger Lipmaa's list of research projects and commercial implementations in secure timestamping](http://kodu.ut.ee/~lipmaa/crypto/link/timestamping/)

#### Oblivious Transfer and Multiparty Secure Computation

-   [Intrusion Detection via Threshold Cryptography](http://theory.stanford.edu/~dabo/ITTC/)

#### Capabilities / Smart Sandboxes

-   [EROS operating system](http://www.eros.org)
-   [E programming language](http://www.erights.org/)

### References

1.  [A01] Agilent Application Note AN 1289, ["The Science of Timekeeping"](http://www.educatorscorner.com/tools/lectures/appnotes/discipline/pdf/5965-7984E.pdf)

2.  [AMPR00] L. Alvisi, D. Malkhi, L. Pierce, and M. Reiter, ["Fault detection for Byzantine quorum systems."](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.12.621&rep=rep1&type=pdf)

3.  [AMPW00] L. Alvisi, D. Malkhi, L. Pierce, M. Reiter, and R. Wright, ["Dynamic Byzantine Quorum Systems"](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.76.4172&rep=rep1&type=pdf)

4.  [B83] M. Ben-Or, "Another advantage of free choice: Completely asynchronous agreement protocols", in Proc. 2nd ACM Symposium on Principles of Distributed Computing (PODC), 1983

5.  [B82] M. Blum, "Coin Flipping by Telephone: A Protocol for Solving Impossible Problems", Proceedings of the 24th IEEE Computer Conference (CompCon), 1982, pp. 133-137. [↩](#refB82)

6.  [BT85] G. Bracha and S. Toueg, "Asynchronous consensus and broadcast protocols", Journal of the ACM, vol. 32, pp. 824-840, Oct. 1985

7.  [CP02] C. Cachin, J. Poritz, ["Secure Intrusion-tolerant Replication on the Internet"](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.20.2828) [↩](#refCP02)

8.  [C01] C. Cachin, ["Distributing Trust on the Internet"](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.26.2399) Conference on dependable systems and networks (DSN-2001). This is an excellent survey of the state of the art in Byzantine-resililient replication as well as presenting his own Byzantine-resilient replication system that uses fair toin cossing. [↩](#refC01)

9.  [C98] C. Cachin , "On the foundations of oblivious transfer", Advances in Cryptology: EUROCRYPT '98, Lecture Notes in Computer Science v. 1403, Kaisa Nyberg, ed., pp. 361-374. Springer-Verlag, 1998.

10. [CT96] T.D. Chandra and S. Toueg, "Unreliable failure detectors for reliable distributed systems", Journal of the ACM, vol. 43, no. 2, pp. 225-267, 1996.

11. [C81] ["Untraceable Electronic Mail, Return Addresses, and Digital Pseudonyms,"]({{url_for('docinfo',%20slug='untraceable-electronic-mail')}}) D. Chaum, Communications of the ACM, vol. 24 no. 2, February, 1981. [↩](#refC81-1) [↩](#refC81-2)

12. [C82] ["Blind Signatures for Untraceable Payments,"]({{url_for('docinfo',%20slug='blind-signatures')}}) D. Chaum, Advances in Cryptology Proceedings of Crypto 82, D. Chaum, R.L. Rivest, & A.T. Sherman (Eds.), Plenum, pp. 199-203. [↩](#refC82-1) [↩](#refC82-2)

13. [C85] ["Online Cash Checks"]({{url_for('slugview',%20slug='online-cash-checks')}}), D. Chaum

14. [CE86] "A Secure and Privacy-Protecting Protocol for Transmitting Personal Information Between Organizations," D. Chaum & J.-H. Evertse, Advances in Cryptology CRYPTO '86, A.M. Odlyzko (Ed.), Springer-Verlag, pp. 118-167.

15. [C89] "Showing Credentials Without Identification: Signatures Transferred Between Unconditionally Unlinkable Pseudonyms," D. Chaum, Accepted but not Presented Auscrypt '89.

16. [C89b] "Privacy Protected Payments: Unconditional Payer and/or Payee Untraceability," D. Chaum, Smart Card 2000, D. Chaum & I. Schaumuller-Bichl (Eds.), North Holland, 1989, pp. 69-93.

17. [CV] "Group Signatures," D. Chaum & E van Heyst, Advances in Cryptology EUROCRYPT '91, D.W. Davies (Ed.), Springer-Verlag, pp. 257-265.

18. [C97] C. Cocks. "Split knowledge generation of RSA paremeters." Presented at the 6th IMA Conference on Coding and Cryptography, Cirencester, England, to appear in the proceedings, December 17–19, 1997.

19. [CGT95] C. Crépeau , J. van de Graaf , and A. Tapp , ["Committed Oblivious Transfer and Private Multi-Party Computations"](http://www.cs.mcgill.ca/~crepeau/GZIP/CGT95.ps); Advances in Cryptology: Proceedings of Crypto '95, Springer-Verlag, pages 110-123, 1995.

20. [C??] F. Cristian [et. al?] on external clock synchronization [↩](#refC--)

21. [CF94] F. Cristian and C. Fetzer, "Probabilistic Internal Clock Synchronization", 13th Symposium on Reliable Distributed Systems", 1994 [↩](#refCF94)

22. [D96] Dohrn-van Rossum, *History of the Hour – Clocks and Modern Temporal Orders*, University of Chicago Press, 1996. [↩](#refD96-1) [↩](#refD96-2) [↩](#refD96-3)

23. [DA01] W. Du, M. Atallah, ["Secure Multi-Party Computation Problems and Their Applications: A Review And Open Problems"](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.11.5269&rep=rep1&type=pdf) (2001), New Security Paradigms Workshop [↩](#ref)

24. [FLP85] M.J. Fischer, N.A. Lynch,, and M.S. Peterson, "Impossibility of distributed consensus with one faulty process", Journal of the ACM, vol 32, pp. 374-382, April 1985. [↩](#refFLP85)

25. [G95] Vicente Goyzueta, ["Cathedral of Qosco City"](http://web.archive.org/web/20040423110545/http://users.bestweb.net/~goyzueta/qosqo/catedral.htm) [↩](#refG95)

26. [HM97] M. Hirt and U. Maurer, "Complete characterization of adversaries tolerable in secure multi-party computation", 16th ACM PODC J. Kilian, *Uses of Randomness in Algorithms and Protocols*, MIT Press 1990.

27. [ISN93] M. Ito, A. Saito and T. Nishizeki. Secret Sharing Scheme Realizing General Access Structure. J. Cryptology, 6 (1993) 15--20.

28. [K90] J. Kilian, *The Use of Randomness in Algorithms and Protocols*, MIT Press 1990 [↩](#refK90)

29. [L78] L. Lamport, "Time, Clocks, and the Ordering of Events in a Distributed System", *Communications of the ACM* 21(7):558-565, July 1978 [↩](#refL78)

30. [L95] Susan K. Langford. "Threshold DSS signatures without a trusted party." In D. Coppersmith, editor, Advances in Cryptology Crypto '95 proceedings, number 963 in LNCS, pages 397 409. Springer-Verlag, 1995. (some context online at http://citeseer.nj.nec.com/context/478327/0)

31. [MR97] D. Maklhi & M. Reiter, ["Byzantine Quorum Systems"](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.40.420&rep=rep1&type=pdf), also in 21st ACM STOC, 1979

32. [MM95] L. E. Moser and P. M. Melliar-Smith, ["Total ordering algorithms for asynchronous Byzantine systems."](http://citeseer.nj.nec.com/context/145304/0) In Proceedings of the 9th International Workshop on Distributed Algorithms, Springer-Verlag, September 1995.

33. [MMA99] L. Moser, P.M. Melliar-Smith, V. Agrawala, ["Total ordering algorithms"](http://portal.acm.org/citation.cfm?id=327298&dl=ACM&coll=portal), Proceedings of the 19th annual conference on Computer Science 1991 , San Antonio, Texas, United States, Pages: 375 - 380 Series-Proceeding-Article Year of Publication: 1999 ISBN:0-89791-382-5 ACM Press New York, NY, USA

34. [MM99] L.E. Moser and P.M. Mellar-Smith, "Byzantine-resistant total ordering algorithms", Information and Computation, vol. 150, pp. 75-111, 1999.

35. [NW96] M. Naor and A. Wool, "Access control and signatures via quorum secret sharing", 3rd ACM Conf. on Computer and Communications Security

36. [MB94] M. Reiter and K. P. Birman. "How to securely replicate services."" ACM Transactions on Programming Languages and Systems, 16(3):986–1009, May 1994.

37. [P91] T.P. Pedersen. "A Threshold Cryptosystem without a Trusted Party."" In Eurocrypt'91, LNCS 547, pages 522--526. Springer-Verlag, 1991.

38. [PSL80] M. Pease, R. Shostak, and L. Lamport, "Reaching Agreement in the Presence of Faults", *Journal of the ACM* 27(2):228-234, April 1980

39. [Rab83] M. Rabin, "Randomized Byzantine Generals," *Proceedings of the IEEE Symposium on the Foundations of Computer Science*, pp. 403-409, IEEE, 1983

40. [SMNTWB02] David Sames, Brian Matt, Brian Niebuhr, Gregg Tally, Brent Whitmore, and David Bakken, "Developing a Heterogeneous Intrusion Tolerant CORBA System", Proceedings of the 2002 International Conference on Dependable Systems & Networks, Washington, D.C., June 23-26, 2002.

41. [Sh79] A. Shamir. "How to share a secret."" In Com. of the ACM, 22(11):612613, 1979. (online at secret.html)

42. [Sh96] B. Schneier, *Applied Cryptography*, 2nd edition, John Wiley & Sons 1996 [↩](#refSh96)

43. [SG98] V. Shoup and R. Gennaro. "Securing Threshold Cryptosystems against Chosen Ciphertext Attack", in Eurocrypt '98, LNCS 1403, pages 1–16. SpringerVerlag, 1998. cf. the extended version for the Journal of Cryptology, available at [http://www.shoup.net/papers/](http://www.shoup.net/papers/)

44. [Sh00] V. Shoup, "Practical threshold signatures", in Advances in Cryptology: EUROCRYPT 2000 (B. Preneel, ed.) vol. 1087 of Lecture Notes in Computer Science, pp. 207-220, Springer, 2000

45. [S97] N. Szabo, ["Contracts With Bearer"]({{url_for('slugview',%20slug='contracts-with-bearer')}})

46. [S97b] N. Szabo, ["The God Protocols"]({{url_for('slugview',%20slug='the-god-protocols')}})

47. [S98] N. Szabo, ["Secure Property Titles with Owner Authority"]({{url_for('slugview',%20slug='secure-property-titles')}}) [↩](#refS98)

48. [S00] N. Szabo, ["Trusted Third Parties are Security Holes"]({{url_for('slugview',%20slug='trusted-third-parties')}})

---

Please send your comments to nszabo (at) law (dot) gwu (dot) edu

Copyright © 2003 by Nick Szabo
 rough draft – quoting or redistribution without permission of the author prohibited

---

*Editor's note: Some links may be broken.*
