# Key Takeaways: Roles and Tools

**Estimated time needed: 5 minutes**

---

## Introduction

The Role and Tools video focused on four aspects of a cybersecurity architect:

- **Role**
- **Mindset**
- **Tools**
- **Domains**

Here are the key takeaways.

---

## Role and Mindset

It all starts with **stakeholders** providing their requirements to the architect. The architect will develop **reference architecture diagrams** that show the relations between the high-level components. The architecture diagrams will be translated into an **IT architecture diagram**.

> **Simple architecture diagram example:** A user accessing a device (desktop/laptop/mobile), which then connects to a web server, which in turn connects with an application server and accesses a database to retrieve information.

The architect then transfers the information to the **engineer**, who will implement the system.

> **Tip:** Architect = Whiteboard | Engineer = Keyboard

### Key Mindset Principle

An architect must understand **how a system works** to assess how and where the system might fail. Always ask:

> *"What do I do to prevent the system from failing?"*

Then figure out how to prevent the failure.

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/modern_security (1).png>)


### Handoff to Engineering

The architect will provide the diagrams to the engineer, who will implement the systems.

> **Note:** Different types of engineers may implement different parts of the architecture. For example, a Database Administrator (DBA) will implement the database, while the network engineer will implement firewalls.

---

## Commonly Used Tools of the Trade for an Architect

In the case of IT, an architect creates **diagrams**. The diagrams act as tools for the architects. The most common ones are:

| Diagram Type                             | Description                                                                                                                |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Business Context Diagrams**      | Provide a high-level line of business view. Show the relationship between different entities in a system                   |
| **System Context Diagrams**        | Decompose the business context diagram further to determine how the entities might look in a system                        |
| **Architecture Overview Diagrams** | Decompose the system context diagrams to determine how the smallest components will look and connect with other components |

> The diagrams are part of the architect's vocabulary. They should be designed so that **any IT architect could understand them**.

### The Cybersecurity Architect's Role

A cybersecurity architect will study the diagrams created by the IT architect and determine how to make the systems and overall architecture **secure and fail-safe**.

The cybersecurity architect will need to use the following as a **checklist**:

- **Five principles of cybersecurity**
- **CIA triad**
- **Frameworks**, such as NIST CSF, providing a checklist to ensure you have covered all your bases

> As a cybersecurity architect, it is your job to apply **all the items in the checklist** to the different diagrams and add security components.

### Critical Timing

It is important to involve the cybersecurity architects in the **Risk Analysis phase** of a project rather than in the implementation phase.

For a secure design and implementation:

1. Apply cybersecurity principles **upfront**
2. Create a **security policy**
3. Follow with an architecture that integrates well with the overall IT architecture

---

## Domains

Each component in the architecture is a **domain**. For example, in the graphic, each component like the user, desktop, and network are all domains that need to be secured from attackers.

> **Additional domain:** A monitoring system that monitors all the domains is also a domain.

If there is a problem, a **response** is needed to ensure that the problem is resolved quickly.
