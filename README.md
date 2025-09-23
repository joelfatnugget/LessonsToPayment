# LessonsToPayment

Come join me as I explore more about the Payments Industry and how it works. I'll be covering one topic every day until I run out of things to talk about.

---

## Day 1: Learning about ISO8583

Today is Day 1 of the entire learning journey. As a start, we will be exploring more about ISO8583 and what it actually is.

ISO stands for the International Organisation for Standardisation—it is a non-governmental organisation that develops and publishes standards that apply globally. It can be for products, services, and systems. This way, everyone who adheres to it knows that there is a certain benchmark to follow in terms of consistency, safety, reliability, and quality across borders and industries.

> *Note: ISO can apply to a lot of things—from Cars (ISO 9001) to Food and Beverage Products (ISO 14001) and Medical Devices (ISO 13485).*

But in this case we are referring to **ISO 8583**, which focuses on the payments industry.

A bit more about the history for ISO 8583: it was used to unite the different payment systems at that point in time.  
**ISO 8583 stands for the International Standard for Financial Transaction Card Originated Interchange Messaging.**  
This was important as it helped to define message format and even communication flows.

---

### Evolution of ISO 8583

| Year  | Changes/Focus                                                                 |
|-------|-------------------------------------------------------------------------------|
| **1987** | - Defined Message Type Indicators (MTI) <br> - Bitmaps & Data Elements <br> - 128 Data Elements |
| **1993** | - Refinements & Clarifications <br> - Flexibility for new Card Processing Services <br> - New Data Elements and Message Types <br> - Improved support for multi-currency, addressed inconsistencies and extended available fields |
| **2003** | - XML Representation (against traditional Bitmap format) <br> - Better definitions for Data Elements (Beyond 128 Data Elements) <br> - Better Support for International Use (Multi-Currency, different card systems) |
| **2023** | - Consolidated Previous Releases and technical revisions. <br> - Restructured the standard for easier maintenance <br> - Greater interoperability between new digital payment systems while maintaining backwards compatibility. |

---

There are also newer ISO standards in the card payments industry!

**New ISO Technology:**  
_**ISO 20022**_  

<img width="400" alt="ISO8583 Illustration" src="https://github.com/user-attachments/assets/c6545b7f-faf5-473d-90ea-c62e5860990c" />

---

## Day 2: 4 Party Model *(To be completed)*

Today’s focus is the **4 Party Model**, which shows how transactions move from buyer to seller.

The best analogy (in Singapore) is buying coffee from Yakun — because Yakun > BreadTalk — so let’s use this familiar experience to break down the 4 Party Model!

---

### The 4 Players
When buying Yakun coffee, think of these 4 stakeholders:
1. **You**  
   Sleep-deprived, surviving on coffee.
2. **Yakun**  
   A business built on caffeinated history (pun intended).
3. **Your Bank**  
   Example: DBS.
4. **Yakun’s Bank**  
   Example: OCBC.
<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/e380133d-038b-4745-8e5e-0255ef6c54b0" />

---

### How the 4 Party Model Works

Here’s the simplified flow:

1. **Card Tap**  
   When you tap your card at the POS Machine, your card details are sent from Yakun’s point-of-sale terminal.

2. **Network Transfer**  
   The POS sends your information to the Payment Networks (Visa, Mastercard, etc.). The network encrypts and forwards it to Yakun’s bank (OCBC), which then routes it back to DBS.

3. **Approval Process**  
   DBS checks your card status, account balance, and flagging for potential fraud. Once verified, it sends an authorization signal back to the POS terminal.

4. **Receipt**  
   The POS terminal prints a receipt and the transaction completes.

[<img width="1560" height="1226" alt="image" src="https://github.com/user-attachments/assets/d9821e7e-7c74-48d8-80d6-e632e79df754" />](https://www.marqeta.com/uk/demystifying-cards-guide/card-payments-ecosystem)

This entire sequence is known as the **Authorization Flow**.

---

## The 3 Key Processes

Each transaction involves three main processes:

| Process        | What Happens                                                  |
|----------------|--------------------------------------------------------------|
| *Authorisation* | Checks if transaction is possible                            |
| *Clearing*      | Exchanges detailed transaction data                          |
| *Settlement*    | Actually moves money between banks                           |

*You, as the consumer, generally only see the Authorisation process. Card declines happen here!*

---

## Digging Deeper: Process Details

### Authorisation Flow  
(Similar to above)

1. Tap card at Yakun.  
2. OCBC sends authorisation request to Visa. (This request is packed with message codes: think “secret language”).  
3. Visa forwards it to DBS.  
4. DBS verifies:  
   - Card is active  
   - Account has sufficient balance  
   - No fraud alerts (e.g. can’t be in China and India at the same time)  
5. DBS approves and sends code back via Visa/Mastercard to OCBC, and finally, to Yakun’s POS terminal.

---

### Clearing

*Typically happens in batches at day’s end.*

1. Yakun sends all approved transactions to OCBC.  
2. OCBC formats and sends them to Visa/Mastercard; this is a **CLEARING file**.  
3. Visa/Mastercard forwards the data to DBS.  
4. DBS records the transactions.

> *Note: The money hasn’t left the bank yet!*

---

### Settlement

This is when the money moves:

1. Visa calculates net amounts owed (like figuring out Splitwise IOUs).  
2. DBS transfers $5 to Visa’s settlement account.  
3. Visa passes funds to OCBC, after deducting network fees.  
4. OCBC deposits the final amount into Yakun’s account.

---

## How Banks & Networks Profit
- Both Visa/Mastercard and the banks take a small fee — think “gas fees” from Crypto/Web3.  
- There are other revenue streams, but transaction fees are the most visible.


---
 
