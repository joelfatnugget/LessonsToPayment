# Table of Content
[Day 1](https://github.com/joelfatnugget/LessonsToPayment/edit/main/README.md#day-1-learning-about-iso8583)   
[Day 2](https://github.com/joelfatnugget/LessonsToPayment/edit/main/README.md#day-2-4-party-model-to-be-completed)  
[Day 3](https://github.com/joelfatnugget/LessonsToPayment/edit/main/README.md#day-3-message-structure)  
[Day 4 - To Be Completed]()  
[Day 5 - To Be Completed]()  
[Day 6 - To Be Completed]()  
[Day 7 - To Be Completed]()  
[Day 8 - To Be Completed]()  
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
