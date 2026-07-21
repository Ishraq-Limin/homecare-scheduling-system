# homecare-scheduling-system
Web and mobile platform for managing carer schedules, client matching, and GPS tracking for a Dublin homecare agency.

A web and mobile platform for managing carer schedules, client matching, GPS tracking, and care notes for a Dublin-based homecare agency.

Project Overview
This project analyses the development, security, reliability, and scalability of a homecare scheduling information system serving elderly and vulnerable clients.
Contents

Development methodology analysis (Agile vs. Waterfall)
Security requirements and GDPR compliance
Reliability and high-availability design
Scalability architecture
Legal and ethical considerations



1. Introduction and Scenario
CareLink Dublin is a small homecare agency based in Dublin, employing 15 carers who provide daily home visits to around 50 elderly clients across the city. The agency currently runs entirely on manual processes: weekly rosters are drawn up on paper, schedule changes are communicated through phone calls and text messages, and carers record care notes in paper diaries kept in clients' homes. This leads to frequent problems, including double-booked carers, missed visits, no way for the office to verify that a carer has actually arrived at a client's home, and lost or illegible care records. Invoicing is done manually at month-end and is often inaccurate. The agency wants a new software system that matches carers to clients, schedules visits automatically, verifies attendance through GPS check-in, stores digital care notes, and handles payments. This report analyses how such a system could be developed, and how it can be made secure, reliable, and scalable.

2. Methodology: Waterfall vs. Agile4

2.1 The Waterfall Model
The Waterfall model is a sequential approach to software development in which the project moves through a fixed series of phases: requirements, design, implementation, testing, and deployment. Each phase must be fully completed before the next begins, and the entire system is specified and planned upfront. This makes Waterfall predictable and easy to document, but also rigid: once development is underway, accommodating new or changed requirements is difficult and costly, as it typically means revisiting earlier phases.

2.2 The Agile Approach
Agile, by contrast, breaks the system down into individual features and tackles them in short, iterative cycles, typically lasting one to four weeks. Working software is delivered at the end of each cycle, and continuous feedback from users and stakeholders shapes what is built next. Rather than fixing all requirements at the start, Agile embraces change, allowing priorities to be reordered as understanding of the problem improves.

2.3 Recommended Approach for CareLink Dublin
Agile is the more suitable methodology for CareLink Dublin. The agency's requirements are almost certain to change as staff move from paper processes to digital ones, and obligations under GDPR will become clearer as the system takes shape rather than being fully understood upfront. Agile also allows incremental delivery: the roster and scheduling module can be released early to deliver immediate value, with GPS check-in, digital care notes, and payments added in later iterations. Crucially, real carers can use the system from the first release and feed their experience directly into subsequent development.
One caveat applies: Agile depends on strong product ownership and disciplined iteration management. Where the budget is tight and fixed, as is likely for a small agency, this discipline is harder to sustain, and scope must be managed carefully to avoid overruns.

3. Security, Reliability and Scalability

3.1 Security
The defining security consideration for CareLink Dublin is the nature of the data itself. The system will store clients' health information — care needs, medication details, and daily care notes — which the GDPR classifies as special-category data under Article 9. This is not ordinary personal data; it belongs to the most protected tier under EU law, and processing it lawfully requires explicit safeguards beyond those applied to routine information (GDPR, Art. 9).
Several techniques address this. First, encryption must be applied both in transit and at rest: data moving between a carer's phone and the server should be encrypted using TLS, and data stored in the database encrypted on disk, so that intercepted traffic or a stolen database is unreadable. Second, role-based access control (RBAC) ensures access is matched to role — a carer sees only their own assigned clients, not all 50; office staff see the full roster; only administrators see everything. Third, multi-factor authentication is essential given that carers log in from personal phones in the field, where devices are more easily lost or compromised. Fourth, audit logging records who accessed which client's data and when, allowing any misuse to be traced and investigated.
These measures should not exist in isolation. An ISO 27001 information security management system provides a structure for organising them and incorporating GDPR obligations into ongoing practice. Among those obligations is breach notification: a personal data breach must be reported to the Data Protection Commission without undue delay and, where feasible, within 72 hours of the agency becoming aware of it (GDPR, Art. 33).

3.2 Reliability
For most businesses, downtime is an inconvenience; for CareLink Dublin it is a safeguarding issue. If the system is unavailable, carers cannot see their rosters, the office cannot confirm that visits to vulnerable elderly clients have taken place, and a missed medication visit may go unnoticed. The system should therefore target 99.99% uptime — equivalent to under an hour of downtime per year — rather than treating availability as a secondary concern.
Several measures support this target. Redundancy and failover mean that no single component is a point of failure: if the primary server goes down, a standby instance takes over automatically, ideally in a different data centre or availability zone. Regular automated backups of the database protect care records and roster data against corruption or loss, and should be tested periodically by actually restoring them — an untested backup is only an assumption. Continuous monitoring and alerting allow the team to detect degraded performance or outages before users report them, so problems are resolved in minutes rather than hours.
Finally, the mobile app should include an offline mode. Carers work in clients' homes across Dublin, where mobile coverage is inconsistent; the app should cache the day's roster and allow check-ins and care notes to be recorded locally, syncing automatically once a connection returns. This ensures that a network dead spot in a client's house does not prevent a visit from being logged, and it also reduces load on the server during peak periods.

3.3 Scalability
CareLink Dublin currently employs 15 carers serving around 50 clients, but the system should be designed to support growth to 100 or more carers operating across several counties. If the architecture cannot scale, success becomes a liability: every new client and carer adds load, and a system designed only for today's numbers will degrade precisely when the business is doing well.
Two broad strategies exist. Vertical scaling means moving the system to a more powerful server — simple, but with a hard ceiling and a single point of failure. Horizontal scaling means adding more servers that share the work, which has no equivalent ceiling and pairs naturally with the redundancy described in Section 

3.2. Horizontal scaling is therefore the better long-term approach, supported by a load balancer that distributes incoming requests — roster lookups, GPS check-ins, note uploads — evenly across the available servers.
Two further techniques reduce the load that must be scaled in the first place. Caching keeps frequently read but rarely changed data, such as the day's rosters and client addresses, in fast memory so that repeated requests do not hit the database. As the client base grows into the thousands, database sharding can partition records across multiple database servers — for example, by county — so that no single database becomes a bottleneck. Together, these measures allow the same system that serves 15 carers in Dublin to serve hundreds nationwide without redesign.
