Subject: Enquiry on Using requestUUID as Sole Idempotent Key for Earmarking and Posting in A&L Transactions
Dear Volante Team,
I hope this email finds you well. My name is [Your Name], and I am [Your Position] at [Your Company]. We have been working with your transaction processing engine and appreciate the robust features it provides for our core banking operations.
To provide some background, our Account & Liquidity (A&L) module currently employs two layers of duplicate transaction detection:
1.  The first layer uses the requestUUID as an idempotent key.
2.  The second layer checks a combination of fields, such as transaction amount, account ID, and others.
However, due to performance bottlenecks identified in our system, we are planning to eliminate the second layer of checks and rely solely on the requestUUID for idempotency in duplicate detection.
With this change in mind, I wanted to enquire about the feasibility and behavior of using the requestUUID as the only idempotent key for earmarking and posting calls within the A&L module. Specifically, we would like to confirm that the Volante engine can effectively leverage the requestUUID in a distributed, multi-pod configuration of the transaction processor. Assuming a resilient system setup, where other pods may resume in-flight transactions (and thus reuse the same requestUUID), please advise on how this would be handled to ensure idempotency without issues like race conditions, duplicate processing, or failures in transaction resumption.
Your insights on this matter would be invaluable in helping us proceed confidently with the optimization. If needed, we can schedule a call to discuss further details or share any relevant system architecture diagrams.
Thank you for your attention to this enquiry. I look forward to your response.
Best regards,