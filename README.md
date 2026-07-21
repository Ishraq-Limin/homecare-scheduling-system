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
