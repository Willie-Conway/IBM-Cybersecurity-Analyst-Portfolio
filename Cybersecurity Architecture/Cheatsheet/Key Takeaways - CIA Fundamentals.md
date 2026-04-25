# Key Takeaways: CIA Fundamentals

**Estimated time needed: 5 minutes**

Here are some key takeaways from the Fundamentals of Confidentiality, Integrity, and Availability video.

---

## Confidentiality

There are two components or technologies involved in ensuring confidentiality: **Access Control** and **Encryption**. Let's review each of these.

### Access Control

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/authorized.png>)

Access Control consists of **authentication** and **authorization**:

- **Authentication** answers the question: *"Who are you?"*
- **Authorization** answers the question: *"Are you allowed to do this or not?"*

If both checks pass, the user is allowed to access the assigned resources.

#### Scenario

| Scenario                                                                                                                                                                      | Example                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Authorized user logs into a system where**multifactor authentication (MFA)** is used for authentication and **role-based access (RBA)** is used for authorization | After successful authentication, the user can access different applications, servers, and databases based on role-based access authorization |

#### Unauthorized User Scenarios

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/unauthorized.png>)

There are two scenarios for unauthorized users:

1. The user is **neither authenticated nor authorized**
2. The user is **authenticated but not authorized**

In either scenario, the user will **not** be able to access the unauthorized items.

### Encryption

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/encryption (1).png>)

**Encryption** is a way to accomplish confidentiality.

When a message is encrypted, only authorized users with the **key** can open it. Unauthorized users may receive the message but will not be able to view the contents.

---

## Integrity

**Integrity** is a quality that says:

- A message is true to itself
- A transaction is true to itself

If a message or transaction gets modified, we can **detect it**. If detected, we will recognize that this should not happen and will take a countermeasure.

### Examples:

- A user should not be allowed to modify or update system logs
- Blockchain should not be modified

### Technologies used:

- **Digital Signature**
- **Message Authentication Code (MAC)**

These cryptographic technologies are used to detect and block any attempt to modify logs or data.

---

## Availability

**Availability** means that authorized users should be able to access systems and resources **when they need it**.

Availability is impacted by **Denial of Service (DoS)** , where an attacker clogs the resources, resulting in the service being denied to an authorized user.

### Variations of DoS:

| Attack Type                                    | Description                                                                                                                                                                                                                    |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Distributed Denial of Service (DDoS)** | Attacker clogs the server not only from their own system but also from other systems they have gained control over                                                                                                             |
| **SYN Flood**                            | Unauthorized user reserves a resource (session). On receipt of an acknowledgement, the user goes silent on this session, then starts another session blocking another resource. This continues until all resources are blocked |

### Result:

> Authorized users cannot access the required service or resource!

### Important:

> Make sure that the system is **up and available** to authorized users when they need it.

---

## Summary

When working on an IT project, one of the things to do is to **cover all your bases**. You can confirm if answers to the following questions are **YES**:

| Question                                                                                                                                  | Check |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ----- |
| Have I met the confidentiality requirements of the project?                                                                               | ☐    |
| Is the sensitive data only available to those who are authorized to see it?                                                               | ☐    |
| Is this system true to itself?                                                                                                            | ☐    |
| Do I have integrity checking so that if someone modifies it or tampers with it, I can be aware of that and know to adjust my trust level? | ☐    |
| Do I have the system available all the time that it's supposed to be available?                                                           | ☐    |
