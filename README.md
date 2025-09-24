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

 ### Day 3: Message Structure: 
 Recap: Remember how we talked about Messages being sent from the POS terminal to Visa's network and then it goes through everything? Yup, today we will be talking about how the systems communicate with each other. 

 You might be thinking it is very complex and difficult such that no one can actually guess it and hack the whole system. But that's where we are wrong, the message is actually rather delicate in the sense that a small change in the number will result in a very different message being sent. 
That being said it is important to know the Message Type Indicator and how it works!
MTI is always a 4 Digit numeric number.
### **MTI Structure: Digit by Digit**
- 1st Digit (Version) = Specifies the ISO8583 Version used to send the message
- 2nd Digit (Message class) = Indicates the general message category
- 3rd Digit (Message Function) = Describes the message's purpose or function
- 4th Digit (Message Origin) = Identifies the message's source or flow stage

_1st Digit_
- 0xxx: 1987's version of ISO8583
- 1xxx: 1993's verison of ISO8583
- 2xxx: 2003's version of ISO8583
- 8xxx: National use
- 9xxx: Private use

_2nd Digit (Message Class)_
- x1xx: Authorisation Message
- x2xx: Financial Message
- x3xx: File Actions
- x4xx: Reversal/Chargeback
- x5xx: Reconciliation
- x6xx: Administrative
- x7xx: Fee Collection
- x8xx: Network Management

_3rd Digit (Message Function)_
- xx0x: Request
- xx1x: Request Response
- xx2x: Advice
- xx3x: Advice response
- xx4x: Notification
- xx5x: Notification acknowledgement
- xx6x: Instruction
- xx7x: Instruction Acknowledgement

_4th Digit (Message Origin)_
- xxx0: Original
- xxx1: Repeat
- xxx2: Response to repeat
- xxx3: Reserved
- xxx4: Reverse

Hence if you were to put it all together, 0100 stands for Authorisation request. 
0110 stands for Authorization Response. 



0200 is the financial transaction request
0210 is financial transaction response
Remember our Yakun example yesterday? When you tap your card, you are sending a 0200 Request. When Visa seeks Authorisation from your bank, it will send back a 0210 Response.

This is slightly tricky because 0100/0110 is actually authorisation messages. Now you might be thinking doesn't that occur for everything? Not quite. 0100/0110 is sent when you are making a pre-authorisation scenario. For example, 0100/0110 is sent when booking a car rental or even a hotel. You will not get charged just yet, but they are checking if your bank account has sufficient money (a threshold in which they will set)

Hence, do not be confused. When you do retail shopping (say when you are buying Labubu or Jellycats), it will be sending 0200/0210 instead as those are financial transaction request/response. Some may choose to use 0100/0110 but not always. 

0420 is a Reversal Advice (message to correct a previous transaction)
0800 is a Network Management Request (Logging on/off or even a heartbeat signal to know the other device is still alive)
0810 is a Network Management Response. 

===
#### Bitmaps
This is where it gets even more technical. Brace yourself.
A bitmap is a string of binary (1 and 0s), you could think of it as a on/off switch. Each bit corresponds to a specific data element number (more about this below). Just know that a bitmap is essentially a map to tell the parser (or the reader) to know what data element is included inside the message. 

You can think of it as bitmap as a paint by number canvas. "If it is a 1, you paint it red. If it is a 2, you paint it blue"
In this case, if a bit is set to 1, the corresponding data element is included in the message. If a bit is set to 0, the data element is not present.

**Bitmap Structure -- TECHNICAL ASPECT (Skip if you want)**
Bitmap has a contains 64 bits. In a message, it has to have a minimum of 1 bitmap and can go all the way up to 3 bitmaps. 
1 bitmap = 64 bits
2 bitmap = 128 bits
3 bitmap = 192 bits

**Single Bitmap (Secondary Bitmap not present)**
So here is how a bitmap looks like ```4210001102C04804```  (Hexadecimal) and this is how it looks like in Binary Number ```0100|0010|0001|0000|0000|0000|0001|0001|0000|0010|1100|0000|0100|1000|0000|0100``` (BINARY NUMBER - 64 Numbers) 
This means that the first hex digit 4 has a binary of 0100, meaning bit 2 is set to 1. 
This means that for Data Element 2, it is present. 
- Data Element 7 is present
- Data element 12 is present
- etc...
 That is how the system will know what Data Elements are present and which Data Elements are not present. 

**Secondary Bitmap Present**
This is what a bitmap with a secondary Bitmap present looks like ```C000000000000000```
Rationale: ```C``` is present because Hex ```C``` starts with binary 1100 (Refer to ascii table), so first bit set to 1 means there is a present of a secondary bitmap. Remember that the secondary Bitmap refers to bits 65 to 128. If bit 65 is present, means Data Element 65 is present.

If this is confusing, REMEMBER. The key is always to convert from Hexadecimal to Binary. It is easier to see it in Binary and 1 and 0s in order for you to know which Data Element is present. 

Hexadecimal --> Binary --> Identification of which Data Element is present

Notice how we can go up to Tertiary Bitmap? It is rarely used.

**Bitmap (Credit Card Aspect)**
Each Bitmap is "map" to a Data Element. Remember Bitmap allows for efficient message construction, avoiding sending fields that aren't needed. This helps as it provides a standardised way to define which fields accompany a transaction based on the transaction type or processing stage.


### Data Elements 
Data elements are individual fields within a Message (Message = MTI + Bitmap + Data Elements).
- Data  Element 2 (DE2) = Primary Account Number (PAN)
- Data Element 3 (DE3) = Processing Code
- Data Element 4 (DE4) = Transaction Amount
- Data Element 7 (DE7) = Transmission Date & Time
etc. There are a lot more fields, you are able to go up to 128 fields (just with secondary bitmap).


The role of Data elements is crucial. They carry all the necessary details needed for the transaction to be processed, authorised, reconciled or even settled. Now whether there is a Data Element or not is based on the Bitmap. 

===
**Slightly more Advance**
_Simpler_
A Data Element has either a fixed length or a variable length. Now Fixed lengths are quite simple, for DE3 (Processing Code)... count 6 digits from start to the end. That's your processing code. Next DE4  has 12 digits, fixed length. 
...|(DE3)|(DE4)
...|000000|000000012345|...
This means that after 6 digits for DE3, it will be 12 digits for DE4 
_Advance_
How then do you deal with the variable lengths and fixed lengths in order to know where to truncate and split them into their data elements?
DE2 has this structure where the first 2 digits indicate the number of digits that follow. 
So for example 161234567890123456 this means that **16**1234567890123456 has 16 digits that follow. Anything else after that, does not belong to DE2.

Say you are given this number ```164532012345678901000000000000012345``` and you are told that this is for DE2 to DE4. Can you split it?

```|16|4532012345678901|000000|000000012345|```


[DE2 - 16 digits | 16 Digits for DE2 | DE3 | DE4|\]

===

In Conclusion: A Message is typically made up of 3 parts. MTI + Bitmap + Data Elements

MTI: Tells you the category of transactions, the class, the function and the origin (Authorisation, Reversal, etc)
Bitmap: Shows you the mapping as to which data elements (aka Fields) are present in the message. 
Data Elements: They tell the actual data containing transaction data like the Primary Account Number (or your  card Number), Transaction Amount etc... These are important, and the presence and order of these fields are dictated by the bitmap, hence the order in which the numbers are being sent is also very important. 

All in all, the Message is one that allows for details to be sent without actually using words to convey it. It uses purely numbers in order to tell a story. A story of whether it is a merchant that wrongly overcharged you, or if it was your haircut that went south. These stories are embedded inside the transaction details. 
