---
title:  'Exposing Your Face Isn't a More Hygienic Way to Pay'
date:   2020-09-21
categories:
  - Artigo
tags:
  - Adicione tags aqui, um item por linha
author:
  - Jon Callas
description: 'Favor colocar aqui uma descrição'
---

```
Tradução por: Traduza_e_coloque_seu_nome_aqui
Formatação e revisão: Matheus Bach, revise_para_estar_aqui
```
[```ver lista de contribuidores```](/about/#contribuidores)

# Exposing Your Face Isn't a More Hygienic Way to Pay

A company called [PopID](https://www.popid.com) has created an identity-management system that uses face recognition. Their first use case is as a system for in-store, point of sale payments using face recognition as authorization for payment.

They are promoting it as a tool for restaurants, [claiming that it is pandemic-friendly because it is contactless](https://www.latimes.com/business/technology/story/2020-08-14/facial-recognition-payment-technology).

Nonetheless, the PopID payment system is less secure than alternatives, unfriendly to privacy, and is likely riskier than other payment alternatives for anyone concerned about catching COVID-19. On top of these issues, PopID is pitching it as a screening tool for COVID-19 infection, another task that it's completely unsuited for.

## Equities issues

It's important that payment systems not disadvantage cash payments, which have the best social equity. Many people are under-banked and in hard times such as these, many people use cash as a way to help them manage their budgets and spending. Cash is also the most privacy-friendly way to pay. As convenient as other systems are, and despite cash not being contactless, we need to protect people's ability to use cash.

PopID is a charge-up-and-spend system. To lower their costs, PopID has its users charge up an account wn ith them using a credit card or debit card, and payments are deducted from that. Charge-and-spend systems are good for the store, and less good for the person using them; they amount to an interest-free loan that the consumer gives the merchant. This is no small thing: [Starbucks, PayPal, and Walmart all have billions in interest-free loans from their customers](https://jpkoning.blogspot.com/2019/08/starbucks-monetary-superpower.html). This further disadvantages people with budgets, as it requires them to give PopID money before it is spent and keep a balance in their system in anticipation of spending it.

PopID also requires their customers to have a smartphone for enrollment-by-selfie, which disadvantages those who don't have one.

To be fair, these issues are largely fixable. PopID could allow someone to enroll without a phone at any payment station. They could allow charge-up with cash, and they could allow direct charge. But for now, the company does not offer these easy solutions.

## Fitness to task

Looking beyond its potentially fixable perpetuation of systematic inequalities, it's important that a system actually do what it's intended to do. PopID is pitching it as a _pandemic-friendly_ system, providing both contactless payments and as a [COVID-19 screening device, using the camera as a temperature sensor](https://www.nytimes.com/2020/05/11/technology/coronavirus-worker-testing-privacy.html). Neither of these is a good idea.

### Temperature scanning with commodity cameras won't work

PopID promotes their system as a temperature scanning device for [employees](https://www.nytimes.com/2020/05/11/technology/coronavirus-worker-testing-privacy.html) and customers alike. Temperature screening itself has limited benefit, as around half the people who have COVID-19 are asymptomatic.

Moreover, accurate temperature screening is expensive and hard. [PopID is not the only organization to promote cheap face recognition with COVID-19 screening as the excuse](https://www.eff.org/deeplinks/2020/04/thermal-imaging-cameras-are-still-dangerous-dragnet-surveillance-cameras). In reality, the cheap camera in a point-of-sale terminal is both inaccurate and intrusive as Jay Stanley of the ACLU [describes in detail](https://www.aclu.org/sites/default/files/field_document/aclu_white_paper_-_temperature_checks.pdf).

There's a wide range in the accuracy of temperature-scanning cameras, in normal human body temperature across a population, and even an individual's temperature based on time of day and their physical activities. Even the best cameras are finicky, not working accurately if people are wearing hats, glasses, or masks, and require the camera to view only one subject at a time.

Speeding up a sandwich shop line _does_ help prevent COVID-19, because [we know that spending too much time too close to other people is the primary mode of transmission](https://elemental.medium.com/the-most-likely-way-youll-get-infected-with-covid-19-30430384e5a5). But, temperature scanning along with payment doesn't help people space themselves out or have shorter contact.

### Face recognition raises COVID-19 risks

PopID pitches their system as good during the pandemic because it is contactless. Yet it is worse than payment alternatives.

PopID's web site shows a picture of a payment terminal, with options to use contactless payment systems such as Apple Pay, Google Pay, and Samsung Pay. Presumably, any contactless credit card could be used. Additionally, a barcode system like the one Starbucks uses is contactless.

![media](/files/2020/09/21/popid-terminal-228.png)

PopID's point of sale terminal

Any of these contactless payment alternatives are much better than PopID from a public health standpoint because they don't require someone to remove their mask. The LA Times article comments parenthetically, "(The software struggles at recognizing faces with masks.)"

Indeed, any contactless payment system has less contact than using cash, yet even cash is low-risk. Almost all COVID-19 transmission is through breathing in virus particles in droplets or aerosols, not from [fomites](https://en.wikipedia.org/wiki/Fomite) that we touch. Moreover, cash is easy to wash in soapy water.

This is a big deal for a supposedly pandemic-friendly system. The most recent restaurant-based superspreading event in the [news](https://www.bloomberg.com/news/articles/2020-08-25/this-starbucks-in-south-korea-became-a-beacon-for-mask-wearing) is particularly relevant. A person in South Korea sat for two hours in a coffee shop under the air conditioning, and spread the disease to twenty-seven other people, who in turn spread it to twenty-nine other people, for a total of fifty-six people. And yet, none of the mask-wearing employees got the virus.

This is particularly relevant to PopID; a contactless system that makes someone take off a mask endangers the other customers. Ironically, if a customer sees a store using PopID, they better be wearing a mask because PopID is requiring them to come off momentarily. Or they could just shop somewhere else.

## Security

PopID brings in new security risks that do not exist in other systems. They have the user's payment information (for charging up the payment store), their phone number (it's part of registration), name, and of course the selfie that's used for face recognition. There's no reason to suppose they're any worse than the cloud services that inevitably lose people information, but no reason to think they're better. Thus, we should assume that eventually a hacker's going to get all that information.

However, being a payment system, there is the obvious additional risk of fraud. PopID says, "[_Your Face now becomes your singular, ultra-secure 'digital token' across all PopID transactions and devices,_](https://www.popid.com/howitworks)" yet that can't possibly be so.

Face recognition systems are well-known to be inaccurate [as NIST recently showed](https://www.nist.gov/news-events/news/2019/12/nist-study-evaluates-effects-race-age-sex-face-recognition-software), particularly with Black, Indigenous, Asian and other People of Color, women, and also Trans or nonbinary people. False positives are common and in a payment system, a false positive means a false charge. PopID says they will confirm any match through the verification process of asking someone their name. To be fair, this is not a _bad_ secondary check but is hardly "ultra-secure." Moreover, it requires every PopID customer to tell the whole store their name (or use a PopID pseudonym).

Lastly, PopID doesn't say how they'll permit someone to dispute charges, an important factor since the credit card industry is regulated with excellent consumer protection. In the event of fraud, it's much easier to be issued a new credit card than a new face.

The end result is that PopID's pay-by-face is less secure than using a contactless card, and less secure than cash.

## Privacy

PopID is an incipient privacy nightmare. The obvious privacy issues of an unregulated payment system that knows where your face has been is only the start of the problem. The LA Times writes:

> But \[CEO of PopID, John\] Miller’s vision for a face-based network goes beyond paying for lunch or checking in to work. After users register for the service, he wants to build a world where they can “use it for everything: at work in the morning to unlock the door, at a restaurant to pay for tacos, then use it to sign in at the gym, for your ticket at the Lakers game that night, and even use it to authenticate your age to buy beers after.”
> 
> “You can imagine lots of things that you can do when you have a big database of faces that people trust,” Miller said.

Nothing more needs to be said. PopID as a payment system is a stalking horse for a face-surveillance panopticon and salable database of trusted faces.

## Conclusion

PopID is less secure and less private than alternative forms of payment, contactless or not. It brings with it a lot of social equity issues that negatively impact marginalized communities. Moreover, any store using PopID and thus requiring other people to remove their masks to pay is exposing you to COVID-19 that you would not otherwise be exposed to.

Most alarmingly, it is also an insecure for-profit surveillance system building a database of you, your face, your purchases, your movements, and your habits.

---
Fonte: https://www.eff.org/deeplinks/2020/09/exposing-your-face-isnt-more-hygienic-way-pay