# Key Takeaways: Five Principles

**Estimated time needed: 5 minutes**

Here are some key takeaways from the Five Principles of Cybersecurity video.

There are five principles of cybersecurity including:

- **Defense in Depth**
- **Least Privilege**
- **Separation of Duties**
- **Security by Design**
- **KISS**

There is also a sixth principle, for anti-security: **Security by Obscurity**.

---

## 1. Defense in Depth

The **Defense in Depth** principle is about creating an obstacle course for the "bad guys." You must include multiple layers of security mechanisms and make the system failsafe. Be it the olden days of castle security or the new age of IT security, Defense in Depth principle remains intact.


![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/castle.png>)

| Security Type   | Security Mechanisms |
| --------------- | ------------------- |
| Old Security    |                     |
| Modern Security |                     |

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/modern_security.png>)

## 2. Principle of Least Privilege

**Principle of Least Privilege** states that access will only be given to those users who need the access to get their work done, and the access must be **time-bound** and **not for perpetuity**.

### Reasons for vulnerabilities include:

- Enabled services that are not used
- Leaving default user accounts as is (e.g., `Admin`)
- **Privilege creep** and **just-in-case access** – users have more access than actually required

> **Privilege creep** – a user may retain access to some applications even after receiving a promotion or moving to a new team.
> **Just-in-case access** – an admin provides access to a user just in case they need it in the future.

### Ways to reduce vulnerabilities:

- Run an **annual recertification campaign** to check all user access and verify it is still appropriate
- Eliminate privilege creep and just-in-case access

---

## 3. Separation of Duties

Make sure there is **no single point of control**. For example, a person who requests access cannot be the approver as well.

> One approach to implement Separation of Duties is to **force collusion**. For example, a lock requires 2 keys to open, and each key is held by a different person.

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/sod1.png>)


---

## 4. Security by Design

**Security must be considered in all phases of architecture**, from start to finish.

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/sbd3.png>)


### Remember:

- Don't wait until the end to think about security.
- Every user in the organization is directly or indirectly responsible for security.
- The network architect or designer must ensure security is built in and users receive a **Secure Out-of-the-Box (OOTB)** solution.

---

## 5. KISS (Keep It Simple, Stupid!)

**System complexity is NOT directly proportional to security!**

- Don't make the system so complex that the user finds it difficult and the "bad guy" finds it easy.
- Remember the maze: If it's harder to do the right thing than the wrong thing, people will do the wrong thing. This increases vulnerability.

---

## Anti-security Principle: Security by Obscurity

Relying on some secret knowledge to make the system safe is a **misconception**. According to **Kerckhoffs's principle**, the cryptosystem should be secure even if everything about the system, except the key, is public knowledge. If security is based on secrecy, we cannot rely on it.

> Implement **black box security** – plaintext goes into a crypto algorithm that we understand and has been published. The only secret is the **key**.
>
