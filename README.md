# Table of Content
[Day 1 - Learning about ISO8583](https://github.com/joelfatnugget/LessonsToPayment/blob/main/README.md#day1-learning-about-iso8583)   
[Day 2 - 4 Party Model](https://github.com/joelfatnugget/LessonsToPayment/blob/main/README.md#day-2-4-party-model)  
[Day 3 - Message Structure](https://github.com/joelfatnugget/LessonsToPayment/blob/main/README.md#day-3-message-structure)  
[Day 4 - Reversal & Advice Messages (Still on MTI & Fields)](https://github.com/joelfatnugget/LessonsToPayment/blob/main/README.md#day-4-reversal--advice-messages-still-on-mti--fields)  
[Day 5 - Data Element 2 & Security Considerations](https://github.com/joelfatnugget/LessonsToPayment/blob/main/README.md#day-5-data-element-2-primary-account-number-and-security-considerations)  
[Day 6 - Data Element 4 and Data Element 7]()  
[Day 7 - Fraud Checks & Risk Scoring]()  
[Day 8 - EMV vs MagStripe]()  
[Day 9 - To Be Completed]()  
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

## Day 2: 4 Party Model 

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

### The 3 Key Processes

Each transaction involves three main processes:

| Process        | What Happens                                                  |
|----------------|--------------------------------------------------------------|
| *Authorisation* | Checks if transaction is possible                            |
| *Clearing*      | Exchanges detailed transaction data                          |
| *Settlement*    | Actually moves money between banks                           |

*You, as the consumer, generally only see the Authorisation process. Card declines happen here!*

---

### Digging Deeper: Process Details

#### Authorisation Flow  
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

#### Clearing

*Typically happens in batches at day’s end.*

1. Yakun sends all approved transactions to OCBC.  
2. OCBC formats and sends them to Visa/Mastercard; this is a **CLEARING file**.  
3. Visa/Mastercard forwards the data to DBS.  
4. DBS records the transactions.

> *Note: The money hasn’t left the bank yet!*

---

#### Settlement

This is when the money moves:

1. Visa calculates net amounts owed (like figuring out Splitwise IOUs).  
2. DBS transfers $5 to Visa’s settlement account.  
3. Visa passes funds to OCBC, after deducting network fees.  
4. OCBC deposits the final amount into Yakun’s account.

---

### How Banks & Networks Profit
- Both Visa/Mastercard and the banks take a small fee — think “gas fees” from Crypto/Web3.  
- There are other revenue streams, but transaction fees are the most visible.


---

## Day 3: Message Structure

**Recap:**  
Remember how we talked about messages being sent from the POS terminal to Visa's network and then moving through all the systems? Today, we will talk about how these systems communicate with each other.

You might think it’s very complex and impossible to guess or hack, but actually, the message is quite delicate. A small change in a number results in a very different message being sent. That’s why it is important to understand the **Message Type Indicator (MTI)** and how it works!

---

### Message Type Indicator (MTI)  
MTI is always a 4-digit numeric number with each digit having a specific meaning:

| Digit Position | Meaning              | Description                          |
|----------------|----------------------|------------------------------------|
| 1st Digit      | Version              | Specifies the ISO8583 version used |
| 2nd Digit      | Message Class        | Indicates the general message type |
| 3rd Digit      | Message Function     | Describes the message’s purpose    |
| 4th Digit      | Message Origin       | Identifies the source or flow stage|

#### 1st Digit (Version)
- 0xxx: 1987's version of ISO8583  
- 1xxx: 1993's version of ISO8583  
- 2xxx: 2003's version of ISO8583  
- 8xxx: National use  
- 9xxx: Private use  

#### 2nd Digit (Message Class)
- x1xx: Authorisation Message  
- x2xx: Financial Message  
- x3xx: File Actions  
- x4xx: Reversal/Chargeback  
- x5xx: Reconciliation  
- x6xx: Administrative  
- x7xx: Fee Collection  
- x8xx: Network Management  

#### 3rd Digit (Message Function)
- xx0x: Request  
- xx1x: Request Response  
- xx2x: Advice  
- xx3x: Advice Response  
- xx4x: Notification  
- xx5x: Notification Acknowledgement  
- xx6x: Instruction  
- xx7x: Instruction Acknowledgement  

#### 4th Digit (Message Origin)
- xxx0: Original  
- xxx1: Repeat  
- xxx2: Response to Repeat  
- xxx3: Reserved  
- xxx4: Reverse  

---

### MTI Examples  
- **0100** = Authorisation Request  
- **0110** = Authorisation Response  
- **0200** = Financial Transaction Request  
- **0210** = Financial Transaction Response  

Example: When you tap your card, you send a 0200 Request. When Visa seeks authorisation from your bank, it sends back a 0210 Response.

Note:  
- 0100/0110 are authorisation messages usually sent during pre-authorisation scenarios (e.g., car rental or hotel booking), checking if the account has sufficient funds.  
- Retail shopping generally uses 0200/0210 financial transaction messages. Some merchants may use 0100/0110 for retail, but it’s not common.

Other useful MTI:  
- 0420: Reversal Advice (to correct a previous transaction)  
- 0800: Network Management Request (log on/off or heartbeat signal)  
- 0810: Network Management Response  

<img width="1272" height="693" alt="image" src="https://github.com/user-attachments/assets/c2a271bb-453d-4e76-b04d-70c878a13c02" />
<img width="790" height="768" alt="image" src="https://github.com/user-attachments/assets/dfa95983-040f-4c7b-baf3-5952cd678408" />

---

### Bitmaps

#### What is a Bitmap?  
A bitmap is a string of binary (1s and 0s), acting like on/off switches. Each bit corresponds to a specific **Data Element number**.  

- Bit set to **1** means the corresponding data element is **included** in the message.  
- Bit set to **0** means it is **not present**.

Think of a bitmap like a paint-by-numbers canvas:  
- If bit 1 is set, include Data Element 1  
- If bit 2 is set, include Data Element 2  
…and so on.

#### Bitmap Structure  
- A bitmap contains 64 bits per block.  
- A message must have **at least 1 bitmap** and can have up to 3 bitmaps (called primary, secondary, and tertiary).  
  - 1 bitmap = 64 bits  
  - 2 bitmaps = 128 bits  
  - 3 bitmaps = 192 bits  

#### Single Bitmap Example  
Hex bitmap: `4210001102C04804`  
Binary (64 bits):  
```
0100|0010|0001|0000|0000|0000|0001|0001|
0000|0010|1100|0000|0100|1000|0000|0100
```

- The first hex digit `4` equals binary `0100` meaning bit 2 is set to 1, so Data Element 2 is present.  
- Bits for Data Element 7, 12, etc., are also present as indicated by the respective bits set to 1.

#### Secondary Bitmap Present  
A bitmap with secondary bitmap presence starts with a hex digit like `C` which in binary is `1100`.  
- The first bit being 1 means the secondary bitmap (bits 65 to 128) is also present.
- For example, if bit 65 is set, Data Element 65 is present.

#### How to Read Bitmap  
**Always convert from Hexadecimal → Binary** to clearly see which bits (data elements) are present.

Tertiary bitmaps exist but are rarely used.

---

### Bitmap and Credit Card Messages  
Each bitmap acts as a map to data elements within the message. This allows efficient construction by sending only necessary fields based on transaction type or stage, instead of sending all data fields.

  <img width="1101" height="502" alt="image" src="https://github.com/user-attachments/assets/39814334-1104-450d-be6f-e2383c568054" />  

<img width="1774" height="446" alt="image" src="https://github.com/user-attachments/assets/c0c64af6-0fde-41c1-a381-6e4c381dc9c4" />  

---

### Data Elements  

Data elements are individual fields in a message:  
- A Message = MTI + Bitmap + Data Elements

Examples:  
- DE2 = Primary Account Number (PAN)  
- DE3 = Processing Code  
- DE4 = Transaction Amount  
- DE7 = Transmission Date & Time  

There can be up to 128 data elements when secondary bitmap is included.

#### Role of Data Elements  
Data elements hold all the necessary transaction details: authorisation, amounts, reconciliation, etc. Their presence depends on the bitmap.

---

### Handling Fixed and Variable Length Data Elements

#### Fixed Length Example  
- DE3 (Processing Code) = fixed 6 digits  
- DE4 (Transaction Amount) = fixed 12 digits  
Example:  
...| DE3 | DE4 |
...|000000|000000012345|

Means 6 digits for DE3, then 12 digits for DE4.

#### Variable Length Example (DE2 - PAN)  
DE2 has variable length indicated by the first 2 digits specifying length.

Example:  
```164532012345678901000000000000012345```

Split:

```
|16|4532012345678901|000000|000000012345|
|-- DE2 --| | DE3 | | DE4 |
```

- `16` indicates DE2 length is 16 digits: `4532012345678901`  
- DE3 is next 6 digits `000000`  
- DE4 is next 12 digits `000000012345`  
<img width="1251" height="442" alt="image" src="https://github.com/user-attachments/assets/8047cf43-e911-42d1-83b1-88f8917a1606" />

---

#### Summary

A message consists of three parts:  
- **MTI:** Defines transaction category, message class, function, and origin (e.g., Authorisation, Reversal)  
- **Bitmap:** Indicates which data elements are present  
- **Data Elements:** Actual transaction data (PAN, amount, timestamp, etc.)  

Messages use numerical data, not text, to efficiently communicate transaction details, telling the story behind every transaction — whether a barber experience gone wrong, or a birthday cake to your wife.

Resources:
[https://www.youtube.com/watch?v=SiCbF8phxhA&t=105s](https://www.youtube.com/watch?v=SiCbF8phxhA)  
[Payment Card Tools - Build your own Bitmap](https://paymentcardtools.com/iso-8583-bitmap)  
[Hexdecimal to Binary](https://www.rapidtables.com/convert/number/hex-to-binary.html?x=4210001102C04804)

---


## Day 4: Reversal & Advice Messages (Still on MTI & Fields)

### Reversal
There are a few instances where Merchants would want to reverse the transaction.

1. Transaction was authorised but cannot be completed  
2. Transaction was completed but there was an error  
3. Acquirer/Merchant must release the hold on funds  

Recall that in Day 3 we talked about MTI and one of the MTI is 0400/0410 which are the reversal codes.  
- **0400** is the request  
- **0410** is the response  

If you think about the flow, using our analogy of buying Kaya toast from Yakun:  

- When you tap your card, the message being sent is **0100 (Transaction Request)** and the response is **0110 (Transaction Response)** → This is the Approved Transaction.  
- When they have accidentally charged you too much, they will call for a reversal of the transaction.  
- They will send **0400 (Reverse Request)** and the POS should ideally receive a **0410 (Reverse Response)**.  

In this particular request/response, it will send quite a few codes, but notably there are:  
- **DE2**: PAN Number (Permanent Account Number)  
- **DE3**: Processing Code  
- **DE4**: Transaction Amount  
- **DE37**: Retrieval Reference No (This is the transaction ID for the Approved Transaction)  
- **DE39**: Response Code  
- **DE90**: Original Data Elements  

Issuer will then use DE37 to find the original authorisation & reverse it.  

**Note:** Reversal Message is different from Advice Messages.  

---

### Advice
Advice Messages usually tell issuers (in this case DBS Bank) about a transaction that has already happened & does not require any authorisation. They usually refer to this message as informational messaging (meaning money does not flow).  

Types of advice messages:  
- **0120** Authorisation Advice  
- **0121** Authorisation Advice Response  
- **0220** Financial Advice  
- **0221** Financial Advice Response  
- **0420** Reversal Advice  
- **0421** Reversal Advice Response  

---

### TLDR
- **Reversal** is to undo a particular transaction.  
  - It happens usually after authorisation but before settlement (clearing phase).  
  - It requires approval from the banks.  
  - Sends a **0400** and receives a **0410** message.  

- **Advice** is informational only.  
  - It happens after the transaction completes.  
  - It does not require approval.  
  - Example flows: send **0120** and receive **0121**, or send **0220** and receive **0221**.  

Hence, there is a big difference between the two. **DO NOT** confuse yourself with these.


---
## Day 5: Data Element 2 (Primary Account Number) and Security considerations

DE2 (PAN) or Data Element 2 - Primary Account Number is one of the most important data elements being transmitted during card payment transaction. As a developer or even just a mere card holder, you need to be very careful in terms of how we utilise DE2. In the hands of the wrong user, it can be detrimental. 

### DE2 (PAN)
- This is Data Element Field that is used to transmit the Cardholder's Primary Account Number  
- It is usually 13 - 19 Digits and Uniquely identifies the Cardholder's payment card. (Hence that is why it is so sensitive)  
- It is present in transaction requests and response message, most notably in any Message Type Indicator involving the MTI (0100, 0200, and 0400)  

> **Fun fact:**  
> The first digit of the PAN is known as the Major Industry Identifier - MII in short (i.e. Mastercard, Visa, American Express)  
> - American Express starts with 3  
> - Visa starts with 4  
> - Mastercard starts with 5  

> **Fun fact continued:**  
> I was curious and went to ask about 1 and 2. Did you know that 1 is for Airline industry and 2 is for Airlines, financial and other future industry assignments?  
>  
> You might be thinking, why? It's simply because in early days the electronic payment systems and card issuers were closely linked with airline companies and travel-related services.  
>  
> Which kind of makes sense because those would be the biggest ticket item you would buy. Payments associated with airline tickets and related travel expenses were a very important use case in the earlier days of the card payments.  
>  
> (Consider searching and reading up about ISO7812)  

![Stripe Image](https://github.com/user-attachments/assets/b2ce31d1-ca1e-4f23-9753-d1554d052a1e)  
*Taken from Stripe's Website*  

The first digit is the Major Industry identifier (MII) while the next 5 - 7 digits are your issuers identification number or the Bank Identification, this identifies the card's issuing institution. Subsequent digits are your individual account identifier. Final Digit is a check digit. It uses **Luhn Algorithm** to validate the PAN's integrity.  

---

### EVEN MORE FUN FACT

#### Magstripe Card
Those old enough will recall that there is a process where you swipe your card and it will transfer the data. This process is call magstripe card. These cards tend to send the "unencrypted" PAN digit across the entire network. This allows for vulnerability to occur and hence it is slowly being phased out. When swiped the magstripe reader reads this static data including the Primary Account Number (PAN) and sends it to the payment processor without encryption.  

Inside Magstripe, there are 3 different tracks:  
- Track 1 and Track 2 contains the PAN and expiration date  
- Track 3 is less frequently used, although in Germany Track 3 is used for debit card transactions  

> **Warning:**  
> This allows for skimming attacks where fraudsters capture the static data and clone a similar card with a similar PAN number and commits fraud that way. Remember the PAN does not change for every transaction.  
>  
> Thus if you were to send the PAN, you are exposing yourself.  

#### EMV Chip Card (Dip) Payment
This is slightly more secure as it will automatically generate a unique cryptographic transaction code for each payment, hence the PAN is being encrypted before sending it across the network. Only the Payment Processor will be able to decrypt everything. Hence, it protects the data in transit and at rest within the merchant's environment.  

#### Tokenization (Most Secured)
This is the most secured as the token replaces PAN during transactions; the real PAN is not being exposed. This is more secured as the tokens are transaction-specific. Real PAN are not being exposed to the merchants/processors during transaction. These are also what powers your Apple Pay and Google Pay (though there are some differences).  

_(I will cover the topic of Tokenization another day, it is big enough for a topic on it's own)_


---

So the next time you are at Yakun making your payment, the safest method to pay the Aunty is through Paywave or Tap to Pay. **Remember cash is our number 1 competitor HAHA.** 

---

## Day 6 (Data Element 4 and Data Element 7) 

### DE4: Amount, Transaction
DE4 actually holds the value of the transaction amount being processed. What is interesting is actually the limits of DE4. How do I make a payment for coffee that is $1 and how do I make a payment for a Handbag that is $10,000? It goes through the exact same process but the question is how then is do I ensure that the system is robust enough to handle both operations. 

Simply put, the DE4 is a 12-digit numerical field hence. For a transaction amount of $23.45, this would mean that the 12 digit would be represented as "000000023450". But naturally the question of how then about the currencies with a lot of 0s (i.e. Korean Won, or Indoensia Rupiah)? Well the answer is always to keep it in the smallest unit of the currency, padded to 12. 

If you are paying for an item in indonesia that cost 1 Million Rupiah, it would be "000100000000" (8 Zeros after 1, and then padded with 0s infront). Thus the maximum price that you can pay at a merchant is 999,999,999,999 Rupiah and that is about 1 trilion Indonesia Rupiah. Which is roughly 78 Million SGD. 

DE4 is closely linked to DE49 due to the currency code. Note: There is no Decimal point as it takes the smallest unit of currency (refers to DE49) and makes that payment. This is essential for clearing and settlement (recall Day 2). Additionally, it can contain zero value for non-financial transactions like balance inquiries where money does not move.

DE4 IS CRUCIAL in card payment systems as it ensures the exact value involved in the transaction is communicated clearly.

### DE7: Transmission Date and Time
This is important as it gives you the timestamp indicating when the transaction message was sent. It has 10 digits, MMDDhhmmss. THis is important as it will combine with other Data Elements (namely DE11 System Trace Audit Number & DE37 Retrieval Reference Number) to give the transaction a rather unique identification. 

It would be critical for synchronisation and for detection of duplicate or even replaced attacks in high-volume transaction. 

Important! DE7 actually helps in terms of fraud detection. It looks at things like Timestamp verification, duplication detection Pattern Analysis, Synchronisation. It is important, as you can't be using the card for a transaction in China at 10am and at 11am you are off in USA using the same card for another transaction. Hence, all these messages must be checked and there has to be some level of fraud detection that goes on almost instantly such that payment can flow. All of this responsibility lies on the shoulders of your payment networks (Visa, Mastercard, American Express etc)

Hence, it is important to know that Both DE4 for Amount and DE7 Transmission Date Time, are critical and vital. These 2 Data elements are necessary to ensure that there is some legitimacy when it comes to transactions. You need to ensure the almost all (if not all) transaction are legitimate and important before it gets processed.


---
# Credit Cards

## Day 7: Fraud Checks & Risk Scoring
Fraud detection is the process of determining potentially unauthorised or suspicious card transaction. I would stop here if I wasn't working in the payment industry, but since I am working in this industry, I will give you more. Fraud detection is the process of determining potentially unauthorised or suspicious card transaction by analysing the data elements within ISO8583 transaction messages. These messages are what we have studied over the past few sessions. From MTI to the different Fields and how they are being sent, these are all important as it gives us clues to determine whether it is a fraud or just merely a proper and legitimate transaction. 

Data Elements (DE) such as transaction type, amount, merchant category code, POS Entry mode etc... are all important as we try to decipher whether a card transaction is legitimate or not. 

Some Key important Data Elements for Fraud detection:
- DE2 --> PAN Number
- DE3 --> Processing Code
- DE4 --> Amount
- DE7 --> Date Time
- DE 18 --> Merchant Category Code (MCC) | 4 Digit Number that classifies the primary product or services. 
- DE22 --> POS Entry Mode | Whether it was contactless, Magstripe or Even Chip Dip
- DE32 --> Acquiring Instituition ID
- DE37 --> Retrieval Reference No | We talked about this previously. It refers to transaction ID 
- DE41 --> Terminal ID
- DE49 --> Currency Code

SO when it comes to Fraud detection, Visa has multiple Fraud Detection tools. 
### 1. Visa Advance Authorisation
VAA is a real-time risk scoring system, this means that every Visa Transaction will be analyzed as it travels through VisaNet (Visa's Network) and produce a risk score. This Risk score will then be assessed by the issuer such that they can accept, decline or challenge transactions. This means that sometimes if your card is decline, it may not be that your bank does not have money but rather that the risk score is too low such that they reject it.

VAA processes billions of data points and uses advanced machine learning models to deliver almost instant insights. This is such a critical function and a lot of money has been poured into this such that Visa can support this infrastructure. The risk score and relevant transaction context are relayed to the issuer during the authorisation flow (recall that there are 3 parts: Authorisation, Clearing and Settlement. 

### 2. Visa Risk Manager
Visa Risk Manager is used by issuers to customize and automate real-time rule management for fraud prevention. Think of it as issuers are allowed to go in and adjust the threshold such that they will allow or reject the transactions. Too high of a threshold, and you end up not being able to sell as much as you would like, you end up turning customers away. Too low of a threshold, and you end up not being able to receive your money. The transaction will fail and you end up losing money eitherways.

Thus it is important to look at the product you are selling and determine the threshold. Naturally, the more expensive your product, the higher you would like to put the threshold such that you allow those who are determined to have enough to purchase and you don't lose money that way. 

VRM allows for you to monitor and adjust fraud strategies almost instantaneously, ensuring coverage across the transaction lifecycle.

What is interesting about these 2 products is that both are done realtime. From the moment you tap, these messages are being sent, AI is checking whether your card is fradulent and then it needs to come back to your POS terminal in a matter of seconds. 

VAA Data is sent to issuers in real-time during the authorisation process. These system use transaction attributes from ISO8583 to get the Risk Score. 

What is even more interesting is that in most regions, Visa actually also does a check on a merchants (i.e the shops selling you the product). Visa requires merchant to use VMSS (Visa Merchant Screening Service) which actually checks Merchants for a history of fraudulent transactions. 

Merchants that commit fraud must be added to VMSS within 1 day notice. 

Furthermore, those activity with higher risk associated tend to require a greater risk score. These activities include:
1. Gambling
2. Adult Entertainment
3. Digital Currencies (Crypto)
4. Quasi-Cash Merchant --> I.e. The act of placing a Wager, purchase of lottery ticket, spread betting etc
5. High Chargeback Merchant --> Travel, Subscription Services etc

It's so interesting because Visa has actually entered the Crypto Space and yet as a company we still feel it is considered a high risk activity. It's so hard to balance everything.


---
Mastercard has it's own version also:
1. Mastercard Decision Intelligence
This is an AI Powered Fraud detection. It uses user history, device data, merchant patterns, network signals to predict the likelihood of fraud. Similar to Visa's Advance Authorisation, if the score falls below the predetermined threshold, it will be flagged for review or even decline. High scores leads to instant approval and a frictionless customer experience. 
2. Consumer Fraud Risk (AI-based Scam detection)
This is similar but it is used to detect and prevent scam-related fraud and social engineering attacks. This focuses on identifying behavioral anomalies, scam patterns and account takeover.


Apologies for not going deep into Mastercard's technologies because they have multiple products. Just that they have multiple products that fragment the entire process and makes it slightly harder to understand. Will try to understand it another day. 

---

## Day 8: EMV vs MagStripe
EMV stands for Europay,Mastercard and Visa. Although it is brands in an acronym, but actually it is referring to the small powerful microprocessor. Magstripe actually refers to the magnetic stripe that is usually on the back of the card and you store data on it. 

Now you can think of Magstripe as a static unencrypted (you see the problem?) data. The moment you swipe your card on the terminal, it will send across your data including your name, account number, and expiraton date. This used to be the default mode of payment in the early 2000s. 

It was only when EMV came out that the adoption of EMV was gradually used. EMV (also generally known as a card 'dip') works when you insert the card into the terminal, this chip then performs a calculation and generates a dynamic, one-time-use code. Some may refer to it as a cryptogram or a digital signature. And Remember it is 1 time use... so it is only valid for that single transaction. 

**The reason why EMV was created**
Magstripe greatest weakness is that it was not 1 time use. The data in the Magstripe never chagnes and thus it makes it incredibly easy to steal and simulate a replay attack (one where the attacker uses your card again). Additionally, other methods like 'Skimming' where a criminal can place a small, illegal device called a "skimmer" over a real card slot. The moment you swipe your card, the skimmer will intercept and read your data. It will then copy the data over to a memory or start to send it via the web back to the hacker's possession. The data can then be cloned onto a blank "dummy" card and then because the data is identical, this cloned card can "impersonate" your card.

EMV Chip was createed to specifically prevent this type of in-person attacks. Because the chip generates it's unique, one-time code, it is somewhat of a self-destructing password. Even if someone manages to intercept, the attacker cannot reuse the code because it has already been used for it's one-time transaction. 

**However**
This is where attackers innovate and they shift to areas where we call it "card-not-present" fraud. This means they are attacking online transaction and payments. For example when you are buying taylor swift concert tickets and you have to insert in your card details, hackers can access that and start their attack. 

It was due to the EMVs that attackers found it difficult to attack in-person transaction and had to shift their plans online. 

*Fun fact*
EMV took awhile to be adopted. Reason? There was a problem with liability. Who were to be at fault if there was a fradulent transaction? Before EMV, if a fradulent transaction happened in the store, the bank was typically responsible for the cost. However, after Oct 2015. The major payment networks (Visa & Mastercard) shifted the rules and implemented the rule that if a merchant were to not have an active EMV chip reader, and they accepted the fraudulent transaction, then the merchant would be held liable for the loss and not the banks themselves. 


#### Why then do we still have Magstripe?
The reason is simply:
1. Backward compatibility.
2. Fallback Mechanism

**Backward Compatibility**
Someone was telling me that in Korea, they are still using Magstripe as the common way of payment. The reason? It was ingrained in them. Their social habits took precedence. Many a times, the locals felt that using the magstripe was the best and safest way to transact. 

**Fallback Mechanism**
If the chip or card reader fails, the terminal oftens falls back onto the magstripe instead. This is less secure, but the transaction can still flow and you can still receive your good. 

However. Magstripe will soon be a thing of the past. By 2033 Mastercard has announced that they will completely remove the magnetic stripes from its new cards as chip and contactless (tap-to-pay) will be the predominant method of payment. 
