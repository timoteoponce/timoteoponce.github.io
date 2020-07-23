{:title "Tale: ETL Component"
 :layout :post
 :tags  ["architecture" "design" "best-practices"]}

## Overview

In this occasion we will see a situation that unexpectedly generated a great design, by purpose and by accident as well.

![Problem](/img/case_study_3_01.png)

Here we've had a customer with a legacy system that stored all its data in a local data source, this is a very old system, written in Fortran, that handles huge amounts of data and it's rarely updated.

As we can already expect, this is not a simple system to integrate with external participants, and that was exactly what they needed. A partner had a website that was well done and wanted to integrated with the legacy system data, meaning that data could be fetch from that system and updated as well.

![Proposed solution - draft 1](/img/case_study_3_02.png)

Our team was asked to provide a solution for this scenario, and here comes out handy the figure of an Architect, we were a young team, with very few years of experience and almost no insight on what to do next.

The Architect took the lead, he designed an ETL (Extract/Transform/Load) component that would act as a mediator between the systems, it would read data from the legacy system and synchronize it to the partner web system, and consequently it would take the data from the partner web system and synchronize it back to the legacy system.

The behavior was designed in this way because the legacy system couldn't be disrupted, a single misbehavior could take the system down, synchronous communication was out of the picture, everything needed to be asynchronous to ensure a stable integration.

![Solution - state 1](/img/case_study_3_03.png)

Our team worked well and delivered the first ETL to production with some small issues, but worked well, the synchronization process between the Legacy and the External partner was performed every two hours and worked really well.

![Problems in legacy](/img/case_study_3_04.png)

But after a few weeks in production the customer and owner of the Legacy system saw a problem, the amount of data changed by the External partner was huge compared to their normal changes rate, the Legacy system was getting slower because of this integration and data synchronization.

Their Legacy system had a great feature for this scenario, they've created a Replica environment that worked for read-only data (which amounted to 90% of the operations) and the original system where data could be written. The new schema solved the problem on their side, but the ETL needed to be updated, it needed to look now at 2 different data sources, with different behaviors.

Our team's Architect took the lead again, he said: "the ETL remains unchanged, we will fix this in the wire". His decision was to put queues in front of the ETL to handle the data traffic, and install agents in the Legacy systems and the External partner system, this agent would monitor the data and communicate with the queues with structured messages, asking for data (read) or performing a data modification (write).

The changes were done in two weeks, the performance remained the same, the ETL performed consistently without changing a line of code, the Legacy system's load was controlled and the External system worked really well and fast.

![Final setup](/img/case_study_3_05.png)

## Backwards Analysis

Thinking back, the project went really well, the development process was smooth, integration was simple and a lot of things that usually go wrong were avoided. Many of these benefits are related to some key decision made by the Architect for the beginning:

  -   Functional programming as main development paradigm
  -   Automated test covering critical cases
  -   Periodical automated build
  -   Asynchronous communication
  -   Ensured communication channel
