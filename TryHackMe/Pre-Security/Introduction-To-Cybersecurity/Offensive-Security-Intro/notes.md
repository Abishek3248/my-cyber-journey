# Offensive Security Intro

**This module introduces the basics of offensive security through a safe, hands-on exercise — hacking your first website in a controlled environment.**

## Introduction
- Offensive security is about adopting the mindset of an attacker.  
- It involves probing systems for weaknesses, exploiting bugs, and bypassing protections to demonstrate potential risks.  
- Ethical hackers apply these techniques responsibly to strengthen defenses.  
- The provided labs are safe, legal, and resettable, making them ideal for experimenting and learning without consequences.  


## Starting the Machine  

The room provides a virtual machine running a simulated banking site (**FakeBank**) for safe, hands-on hacking practice.  

## My First Hack

### Concept Learned
- Hidden URLs in web applications can expose sensitive functionality.
- Directory brute-forcing helps discover such URLs using wordlists.

### Commands
- dirb http://fakebank.thm

### Notes / Experience
- First hands-on hack: used dirb to enumerate directories on the FakeBank app.
- Found useful endpoints such as /bank-deposit and /images — potential places to investigate further.
- Reinforced that attackers often rely on predictable paths; developers leaving default or obvious pages can be risky.
- his module is mostly conceptual with short, practical exercises — good for building a baseline before deeper exploitation techniques.

## Exploiting Hidden Endpoints

### Concept Learned
- Exploitation of exposed functionality: secret endpoints can enable unauthorized actions (e.g., adding funds).  
- Necessity of server-side authorization and input validation — client-side checks alone are insufficient.  
- Real-world impact: exposed admin-like pages can be abused to manipulate user data, steal funds, escalate privileges, or pivot to other attacks.

### Exploit Procedure
- Open the discovered endpoint in the browser:  
  `http://fakebank.thm/bank-deposit`  
- Submit the deposit form to add **$2000** to account **8881**.  
- Return to the account page to confirm the balance update and the successful manipulation.

### Notes / My Experience
- The deposit endpoint accepted the action without proper authentication/authorization checks, allowing unauthorized modification of account balances.  
- This exercise demonstrated how a single exposed URL can have severe consequences for data integrity and financial security.  
- Ethical reminder: only perform such tests in authorized labs; report real-world findings responsibly.


## Mitigations
- Enforce server-side authorization for all sensitive endpoints (verify the acting user's identity and permissions).  
- Validate and sanitize all input server-side; never trust client-supplied data.  
- Implement CSRF protections and require authenticators for state-changing actions.  
- Log and monitor high-risk operations and apply least-privilege access controls and rate limiting.

## Key Takeaway:
- Offensive security = thinking like an attacker to improve security.  
- The first step in this journey is learning how hackers operate in order to defend effectively. 
- basic reconnaissance: even simple hidden endpoints can reveal sensitive functionality.
- Server-side authorization is essential; unprotected endpoints can be easily exploited by attackers.
- Directory enumeration and form testing are simple but effective ways to uncover vulnerabilities.
- Understanding how an attacker thinks helps in designing secure systems and mitigating risks.
- Hands-on exercises show that practical hacking starts small, often by exploring what seems trivial, like hidden pages.
- Always validate input and enforce strict access control to protect sensitive actions and user data.
- Experience gained highlights the importance of ethical hacking to proactively secure applications.


