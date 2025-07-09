# DO288 Containerized Example Applications

Here’s a clear, structured meeting agenda based on your notes. The goal is to drive alignment around making PODS the authoritative source for all payment statuses and related event data.

⸻

Meeting Agenda: Establishing PODS as the Authoritative Source for Payments

Date: [Insert Date]
Time: [Insert Time]
Duration: [e.g., 60 minutes]
Attendees: Ram, Daiva, Libby, Raj, Amit, Byron (optional), [Add others as needed]
Facilitator: [Insert Name]

⸻

1. Opening and Purpose (5 mins)
	•	Quick context-setting
	•	Objective: Discuss and align on making PODS the single authoritative source for all payment statuses and events across payment engines.

⸻

2. Current State Overview (10 mins)
	•	Payment Router behavior
	•	When it is invoked, and examples of non-router use cases (e.g., LMS, mortgage disbursements)
	•	Orchestration Layers
	•	SPS vs. GMM: Clarifying roles and responsibilities

⸻

3. Event Flow and Status Tracking (15 mins)
	•	View Intellect / Liquidity Needs
	•	Centralized status updates (push vs pull)
	•	Importance of a consistent API or Kafka-based delivery mechanism
	•	Current Gaps
	•	Engines not aligned to emit standardized events
	•	LMS missing listener service and event publishing
	•	Proposed Direction
	•	Normalize all vendor-specific events into Pack 002 format
	•	PODS to subscribe to these via Kafka

⸻

4. PODS as the Central Source (15 mins)
	•	Why PODS?
	•	Global view of all payments regardless of origin (ACH, Fedwire, RBC Book, etc.)
	•	Reduces complexity for consumers by offering a single interface
	•	ODR Integration
	•	ODR as a replica of PODS for RBC Clear context
	•	Confirm pattern of events flowing from ODR → PODS
	•	Target State
	•	All engines emit normalized events → ODR/WallPage → PODS
	•	Push model preferred; pull allowed only in low-volume scenarios

⸻

5. Implementation & Ownership Discussion (10 mins)
	•	Who owns what:
	•	Raj: FedWire, ACH, Book-to-book
	•	Amit: Consumer of events; handles push/pull logic
	•	Payment engine teams: Emit and align events to PODS
	•	Estimation Considerations
	•	Work effort to include listener services, event transformation, and publishing
	•	Avoid estimating per payment; focus on infrastructure and integration

⸻

6. Action Items & Next Steps (5 mins)
	•	Add Daiva to the working group
	•	Identify PODS schema versioning and publishing timelines
	•	Schedule follow-up meeting with all stakeholders
	•	Define success metrics and timelines for Pack 002 normalization (6–8 months goal)

⸻

Pre-Reads / Pre-Work
	•	Review current payment status flows for each engine
	•	Come prepared to discuss what event data is currently emitted and what’s missing

⸻

Let me know if you want a slide version or an editable doc version of this.