---
layout: post
title:  "Coffee Shop Loyality Program - Part I"
---

# 1) Problem
Today, I went to my local coffee shop and ordered a latte. The staff asked me to mark the loyality card if I have any. I told her that I have it but left it at home. Then she told me that every customer tells the same thing and she could mark it in my next appearance. This led me questioning whether such thing (forgetting loyality card at home) can be prevented.

I don't want to carry anything more at my wallet or bag, so keeping the card with me all the time is not an option for me (obviously for others too).

But everybody carries their phones all the time, so can't we use those? Starbucks developed a mobile app for this but why develop another for my local coffee shop?

Then I wondered if blockchain can be used. This would be a challange for me to build a complete product (at least MVP version).

So in this post, I am sharing my chain of thought for the problem: how I can develop a customer loyality program using blockchain.
In future posts, I will be sharing my experiences on development of this program.


# 2) Keywords
A quick search led me some of these keywords:
- loyality program / token
- web3 loyality scheme
- token redemption (for discounts, free products, special offers)
- NFT

# 3) Related links
- [Making blockchain real for customer loyalty rewards programs - Deloitte](https://www2.deloitte.com/us/en/pages/financial-services/articles/making-blockchain-real-customer-loyalty-rewards-programs.html)
- [The Power of Web3 and Blockchain](https://news.fuse.io/revolutionizing-loyalty-programs-the-power-of-web3-and-blockchain/)
- [Other companies adopting loyality programs](https://blog.usetada.com/en/companies-adopting-blockchain-loyalty-programs) - like airlines, restaurants
- [Raise of blockchain loyality programs](https://blaize.tech/services/blockchain-integration/blockchain-loyalty-programs/)


# 4) Requirements
These requirements are determined solely by me, without gathering with customers or coffee shop's owner.

- low transaction fees (less than 50 cents)
- fast (transactions are completed within less than one minute)
- mobile phones shall be used, but no custom mobile app shall be developed
    - only frontend as a web app shall be developed
- user friendly, frictionless onboarding for people who don't have experience with any blockchain technologies.
    - users should be guided for wallet creation & usage, and those operations should be simplest
    
    - common wallet apps like Metamask is preferred since many of the customers do not have enough experience, nor want to install another app to their phones
- easy to use by coffee shop personnel who will verify the customers' rewards
- all transaction fees shall be paid by coffee shop's wallet
- coffee shop staff can have their own accounts different than coffee shop owner's
- easy and fast development


# 5) So which blockchain platform is best for such use cases?
Quick search using ChatGPT, several projects are offered such as;
- **Stellar**
- **Solana**
- **Polygon**
- **Binance Smart Chain (BSC)**
- **EOSIO**
- **Tezos**

I know this is a very bad architectural decision making but I am opting out the projects that I do not have prior knowledge. Keeping Solana, Polygon and BSC.

All of them provide low transaction fees and high speed. But in terms of customer onboarding, Polygon and BSC are better alternatives since they are supported in Metamask. But for Solana, another mobile app needs to be installed as a wallet app, which can cause friction. Remember, one of my requirement is easy integration for people with little experience in blockchain technologies.

However, I stumbled another wallet called Phantom, which can replace Metamask, I will look into that. If Phantom wallet is used, then Solana can still be an option.

BSC has an advantage since probably most of customers have Binance app installed in Turkey. However, Binance has a separate app (Binance TR) to operate in Turkey, which does not support such features yet. Hence, I cannot use this advantage.

So Polygon is the final candidate. It has a good community, which will make my development easier.


# 6) Before implementation

I prefer to determine example use cases before doing any development.

After that, I want to visualize those operations from each user (role)'s perspective. Hence, I prefer starting front-end mockups before any backend development.

I did not generate any mockups yet, since I need to speculate about possible features first.


# 7) Minimal Viable Product

Starting from frontend, only single feature

⇒ *after each 10 product purchase, customers can redeem 1 free product as a reward*

I can develop a responsive Next.js app and free Vercel deployments can be used!

Basic features:
- 1 product type (generic like "coffee", not specific like "americano" or "latte")
- 3 user roles: customer, staff, shop owner
- Each user is initially hard-coded. Customers can:
    - purchase a product
    - redeem a reward
- Conditions for reward redemption:
    1. Calculate non-redeemed reward count
        - customer may have purchased 32 products with no redemption, so they can have total 3 free products (in any time)
            - example flow for tests ⇒ 32 purchase + 1 redemption + 1 purchase + 1 redemption + 7 purchase + 1 redemption + 1 redemption
    2. If user has not-redeemed reward → allow redemption:
        - coffee shop's wallet will pay the fee for NFT minting or transaction
 


# 8) Next Features

- Onboarding for users without a wallet/metamask etc
    - QR code scanning
- Customer and staff can see
    - Customer's purchase and reward history
- Staff
    - Can view history of particular customer
    - Verify/approve reward by scanning a QR after customer has successfully redeemed the reward
    - Add/remove new products:
        - If carrot cake is added to the menu, staff can insert to blockchain (or remove it)
    - Generate different reward types:
        - 50% discount for products X, Y, or Z
        - For product X: 1 purchase - 1 free
    - generate time-limited rewards:
        - 50% discount on all cakes until the end of the day/tomorrow night
        - 1 free americano for any product purchase between April 20 and 27
- Owner
    - All things staff can do, plus:
        - Add/remove staffs
        - Deposit or withdraw money from/to coffee shop wallet
    - See stats like:
        - How many rewards have given in this month
        - How many purchases have done in this month


# 9) Next
- Should I use Phantom wallet instead of Metamask?
- Why [starbucks is dropping its nft program](https://www.ccn.com/news/starbucks-odyssey-nft-beta-web3s-potential-bolster-loyalty-programs/)?
- Similar projects in Github that are already developed
- See [Open Loyality](https://www.openloyalty.io/insider/the-rise-of-blockchain-loyalty-programs-with-cezary-olejarczyk) - uses Hyperledger fabric
- Find out **the average fee in peak times** to calculate possible cost

