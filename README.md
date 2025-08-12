# DO288 Containerized Example Applications

Here’s the thing about your Liquidity Management System sweep use case:

1. Can you use PaymentInformation.CategoryPurpose.Code for LMS sweep?
Yes, you can — if you treat Category Purpose as a high-level business reason for the payment. ISO 20022’s CategoryPurpose (in PmtInf/CtgyPurp/Cd) is intended for indicating the underlying category of the payment — things like SALA (salary), TREA (treasury), SUPP (supplier payment), DIVI (dividends), PENS (pensions).

For sweeps, the most relevant standard code in the ISO external code list is:

SWPT — Sweep Transaction

“Movement of funds for liquidity management purposes between two accounts belonging to the same customer.”

This fits your LMS sweep exactly.

So if your LMS is instructing a sweep via your Router API, you can populate:

xml
Copy
Edit
<PmtInf>
   ...
   <CtgyPurp>
      <Cd>SWPT</Cd>
   </CtgyPurp>
</PmtInf>
Pros

Standards-aligned (any ISO 20022-aware recipient will understand it’s a sweep)

Allows downstream systems (fraud, analytics, reporting) to filter/route on category without parsing free text

Cons

It’s descriptive, but not authoritative for who initiated — that’s InitgPty

2. Alternative/additional tags you might want to use
If you want a system identifier for routing or analytics beyond the standard category, you could also:

InitiatingParty in GrpHdr — Set to your LMS as the actual initiator (<Nm>Liquidity Management System</Nm> or OrgId with some identifier).

PaymentTypeInformation.LocalInstrument.Code — If you want an internal routing key that’s not exposed as a business category. Could use a bank-specific local instrument code for "LMS-SWEEP".

InstructionForNextAgent (if bank-to-bank) — For additional processing instructions, though not the primary place for business category.

Purpose.Code (in transaction) — Distinguishes the purpose of a single transaction, whereas CategoryPurpose applies to the whole batch.

3. My recommendation for your Router API schema
For an LMS sweep via your ISO 20022 request:

GrpHdr.InitgPty → LMS entity ID (so you always know who the true initiator is)

PmtInf.CtgyPurp.Cd → SWPT (standard sweep code)

Optionally: PmtTpInf.LclInstrm.Cd → internal LMS code if you need to route differently than just "sweep"

This way:

Your downstream engines can recognize sweeps without custom parsing

Fraud/AML can distinguish them from normal wires/ACH

You keep your schema fully standards-compliant

If you want, I can give you a full XML snippet showing exactly how an LMS sweep would look in your Router API’s ISO 20022 payload — ready to send to FED, SWIFT, ACH, etc.
Do you want me to prepare that?














ChatGPT can make mistakes. Check important info. See Cookie Preferences.

