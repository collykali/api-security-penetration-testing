# API Security & Penetration Testing

**Author:** Collins Onyeka
**Focus:** API Security | Penetration Testing | Cybersecurity

> A hands-on learning journey into API reconnaissance, endpoint analysis, injection testing, vulnerability chaining, and AI-powered API security.

---

## Table of Contents

* [About This Repository](#about-this-repository)
* [Objectives](#objectives)
* [Methodology](#methodology)
* [Micro-Quest 1: How API Pen-Testers Approach Systems](#micro-quest-1-how-api-pen-testers-approach-systems)
* [Micro-Quest 2: Thinking Like an Attacker — Identifying Injection](#micro-quest-2-thinking-like-an-attacker--identifying-injection)
* [Micro-Quest 3: Why API Breaches Happen Through Chains](#micro-quest-3-why-api-breaches-happen-through-chains)
* [Micro-Quest 4: Securing AI-Powered APIs](#micro-quest-4-securing-ai-powered-apis)
* [Micro-Quest 5: API Security Is Not a Feature](#micro-quest-5-api-security-is-not-a-feature)
* [Tools](#tools)
* [Key Lessons](#key-lessons)
* [Practical Work](#practical-work)
* [Ethical Testing](#ethical-testing)
* [References](#references)

---

## About This Repository

This repository documents my hands-on learning journey into API security and penetration testing.

The focus is not simply on running security tools or identifying individual vulnerabilities. I am using practical exercises to understand how APIs behave, where security assumptions can fail, how vulnerabilities can interact, and how security findings should be investigated and documented.

The work covers API reconnaissance, endpoint discovery, HTTP request analysis, injection testing, authorization weaknesses, vulnerability chaining, and the security challenges introduced by AI-powered APIs.

All practical testing documented here is performed in authorised training or laboratory environments.

---

## Objectives

The objectives of this project are to develop practical understanding of:

* API attack-surface discovery
* HTTP request and response analysis
* Authentication and authorization testing
* API endpoint enumeration
* Input validation and injection testing
* Broken Object Level Authorization (BOLA)
* Vulnerability chaining
* API fuzzing
* Legacy and undocumented API discovery
* AI-powered API security
* Security documentation and reporting

The broader objective is to develop the ability to reason about an application from both the developer's and attacker's perspectives.

---

## Methodology

My approach to API security testing follows a simple cycle:

```text
Reconnaissance
      ↓
Understand the Application
      ↓
Establish a Baseline
      ↓
Test Individual Components
      ↓
Analyse Anomalies
      ↓
Validate Findings
      ↓
Assess Impact
      ↓
Document and Recommend Remediation
```

The important part of this process is not the number of tools used.

It is understanding why a particular test is being performed and what the resulting behaviour means.

---

# Micro-Quest 1: How API Pen-Testers Approach Systems

API penetration testing starts before payloads are injected.

The first task is understanding the attack surface.

### Reconnaissance

Depending on the authorised environment, reconnaissance can include:

* OSINT
* DNS and subdomain enumeration
* Asset discovery
* API documentation review
* Historical endpoint discovery
* Service enumeration
* Endpoint discovery

Tools such as Amass, Kiterunner, Shodan and the Wayback Machine can help identify assets and endpoints that may otherwise be overlooked.

The important question is not simply:

> "How many endpoints can I find?"

It is:

> "What does this endpoint tell me about the application?"

An apparently insignificant endpoint can reveal object identifiers, naming conventions, authentication assumptions, or older functionality.

### Testing

Once the attack surface is understood, individual endpoints can be examined.

This may include:

* Request and response analysis
* Authentication testing
* Authorization testing
* Parameter manipulation
* Input validation
* Fuzzing
* Error analysis
* Business-logic testing

Burp Suite is particularly useful during this stage because it allows HTTP/HTTPS traffic to be intercepted, inspected, modified and replayed.

However, Burp Suite does not determine whether a behaviour is actually a vulnerability.

The tester has to interpret the behaviour within the context of the application.

### Establishing a Baseline

One mistake beginners can make is immediately injecting payloads without first understanding normal application behaviour.

A baseline gives the tester something to compare against.

A useful process is:

```text
Observe → Understand → Modify → Compare → Investigate
```

A different status code or response length is not automatically a vulnerability.

It is an observation that requires investigation.

### Forgotten Endpoints

Legacy and undocumented APIs deserve attention.

An organisation may deploy a newer API while older endpoints remain accessible.

These endpoints may contain:

* Outdated authentication
* Inconsistent authorization
* Excessive data exposure
* Abandoned functionality
* Older dependencies

This makes asset management an important part of API security.

---

# Micro-Quest 2: Thinking Like an Attacker — Identifying Injection

Injection becomes easier to understand when an input field is viewed as more than a place where a user enters text.

The important question becomes:

> "Where does this input go after the server receives it?"

An API parameter may eventually interact with:

* SQL databases
* NoSQL databases
* Operating-system commands
* Template engines
* Application interpreters

If untrusted input reaches an interpreter without appropriate controls, it may alter the intended operation.

### What I Look For

During authorised testing, useful indicators can include:

* Unexpected status codes
* Response-length changes
* Database errors
* Stack traces
* Unexpected response structures
* Timing differences
* Changes in authentication behaviour

Burp Suite and fuzzing tools can automate repetitive testing.

The more important skill is interpreting the results.

A changed response does not immediately mean:

> "This is SQL injection."

A better conclusion is:

> "Something changed when the input changed. I need to understand why."

### Testing Logic

My reasoning process is:

1. Establish the original response.
2. Modify one variable.
3. Observe the difference.
4. Repeat the behaviour.
5. Determine what component is reacting.
6. Establish whether there is security impact.
7. Document the evidence.

This approach helps reduce false positives.

### Defensive Controls

Common defensive measures include:

* Parameterized queries
* Strict input validation
* Schema validation
* Appropriate type enforcement
* Least-privilege database accounts
* Safe command execution
* Secure error handling

The goal is not simply to block known payloads.

The goal is to prevent untrusted data from changing the meaning of an operation.

---

# Micro-Quest 3: Why API Breaches Happen Through Chains

One of the most important lessons from API security is that vulnerabilities should not always be considered independently.

Consider a simplified attack path:

```text
Legacy Endpoint
      ↓
Information Exposure
      ↓
User/Object Identifier
      ↓
Broken Object Level Authorization
      ↓
Unauthorised Object Access
      ↓
Sensitive Data Exposure
```

An information disclosure might appear limited when considered on its own.

If the exposed information can be used to exploit an authorization weakness elsewhere, its security significance changes.

### BOLA

Broken Object Level Authorization occurs when an API fails to properly verify whether the requesting user is authorised to access a specific object.

Authentication answers:

> "Who are you?"

Authorization answers:

> "What are you allowed to access?"

These are different controls.

A user being successfully authenticated does not mean that the user should be able to access every object exposed by an API.

### Thinking in Attack Paths

Instead of asking only:

> "How serious is this vulnerability?"

I also ask:

> "What could this enable when combined with another weakness?"

This is one of the areas where API penetration testing becomes more interesting than simply checking boxes on a vulnerability list.

---

# Micro-Quest 4: Securing AI-Powered APIs

AI-powered applications introduce another layer to API security.

An LLM may accept natural-language input and produce output that influences tools, functions or backend systems.

A simplified architecture may look like:

```text
User Input
     ↓
LLM Application
     ↓
Tool / Function
     ↓
Backend API
     ↓
Database
```

This creates a new trust boundary.

### Prompt Injection

Prompt injection occurs when crafted input influences an AI system to behave contrary to the application's intended instructions or security controls.

The risk becomes more significant when the model can interact with external tools or backend functionality.

The security concern is not simply that the model produces unexpected text.

The concern is what that output is allowed to trigger.

### Safer Architecture

A more controlled architecture separates model output from authorization:

```text
User Input
     ↓
LLM
     ↓
Structured Output
     ↓
Schema Validation
     ↓
Authorization Check
     ↓
Approved Tool/API Operation
     ↓
Backend System
```

The critical distinction is:

**What the model wants to do**

versus

**What the application allows it to do.**

### Security Controls

AI-powered APIs should consider:

* Strict schema validation
* Tool-level authorization
* Least-privilege access
* Sandboxing
* Output validation
* Sensitive-data controls
* Rate limiting
* Audit logging
* Explicit confirmation for high-impact actions

An LLM should not be treated as the authorization boundary.

---

# Micro-Quest 5: API Security Is Not a Feature

The biggest lesson from these exercises is that API security cannot be reduced to adding authentication and considering the system secure.

An endpoint can be:

* Authenticated but improperly authorised
* Encrypted but vulnerable to injection
* Secure today but forgotten tomorrow
* Safe in isolation but vulnerable when chained with another weakness
* Properly implemented but exposed through an undocumented legacy API

Security therefore has to be considered throughout the API lifecycle.

### Developer Thinking vs Security Thinking

A developer may ask:

> "Does this endpoint perform its intended function?"

A security tester asks additional questions:

> "What happens if I change the object ID?"

> "What happens if I remove this parameter?"

> "What happens if I change the data type?"

> "What happens if I replay the request?"

> "What happens when another authorised user sends it?"

> "What happens if this endpoint was never intended to be public?"

> "What happens when this weakness is combined with another one?"

This shift in perspective is one of the most valuable skills I am developing through API security practice.

---

# Tools

| Tool                      | Purpose                                              |
| ------------------------- | ---------------------------------------------------- |
| Kali Linux                | Security testing environment                         |
| Burp Suite                | HTTP interception, request manipulation and analysis |
| Nmap                      | Network and service reconnaissance                   |
| Kiterunner                | API endpoint discovery                               |
| ffuf / WFuzz              | Fuzzing and endpoint discovery                       |
| Amass                     | Asset and subdomain enumeration                      |
| Wayback Machine           | Historical endpoint discovery                        |
| OWASP API Security Top 10 | API security reference and classification            |

Tools provide visibility and automation.

They do not provide understanding.

That remains the responsibility of the tester.

---

# Key Lessons

### 1. Reconnaissance matters

You cannot properly assess what you cannot see.

### 2. Establish a baseline

Understanding normal behaviour makes abnormal behaviour easier to identify.

### 3. Authentication is not authorization

Knowing who a user is does not automatically determine what they can access.

### 4. Vulnerabilities can interact

A vulnerability's significance can change when it becomes part of a larger attack path.

### 5. Legacy APIs matter

Old endpoints can remain security-relevant long after their original purpose has been forgotten.

### 6. Tools do not replace reasoning

A tool can show a changed response.

It cannot explain the business meaning behind that change.

### 7. AI introduces another trust boundary

LLM output should not bypass deterministic authorization and validation controls.

### 8. Security is continuous

An API is not secure simply because it passed one security test.

---

# Practical Work

This section will be expanded as I complete additional authorised laboratory exercises.

Future documentation will include:

* API reconnaissance
* Endpoint enumeration
* Burp Suite traffic analysis
* Injection testing
* BOLA testing
* API fuzzing
* Vulnerability validation
* Nmap NSE scripting
* AI API security testing
* Security findings and remediation recommendations

Where appropriate, screenshots and technical evidence will be included to demonstrate the practical work behind each finding.

---

# Ethical Testing

All testing documented in this repository is intended for:

* Personal laboratories
* CTF environments
* Deliberately vulnerable applications
* Training platforms
* Systems where explicit authorization has been granted

Do not scan, fuzz, exploit or otherwise test systems without permission.

Responsible security research begins with authorization.

---

# References

* [OWASP API Security Project](https://owasp.org/www-project-api-security/)
* [OWASP API Security Top 10](https://owasp.org/API-Security/)
* [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
* [PortSwigger Web Security Academy](https://portswigger.net/web-security)
* [Nmap Documentation](https://nmap.org/docs.html)
* [MITRE CWE](https://cwe.mitre.org/)

---

# About the Author

I am Collins Onyeka, a cybersecurity enthusiast building practical experience through hands-on security labs, API security testing, digital forensics, network security and security automation.

This repository is a record of my learning process, practical investigations and technical development.

I am particularly interested in understanding not only how vulnerabilities work, but also **why they occur, how they can be chained, how they affect real systems, and how they can be prevented.**

> **Theory gives me the foundation. Practical testing teaches me how systems actually behave.**
