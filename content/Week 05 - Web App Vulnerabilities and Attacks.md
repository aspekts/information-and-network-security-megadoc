---
title: Week 05 - Web App Vulnerabilities and Attacks
date: 2025-12-14
tags:
  - web-security
  - attacks
  - vulnerabilities
  - code-analysis
aliases:
  - SQL Injection
  - XSS
  - CSRF
  - Input Validation
summary: Common web exploits including SQLi and Cross-Site Scripting, with code-level mitigation examples.
---
## Key Terms

| Term                                         | Definition                                                                                                                                                                                                                             | Exam Context/Example                                                                                                                                                                                                                                   |
| :------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Unauthorised hacking/“testing”/attacking** | Carrying out activities against computer systems without authorization, which is illegal.                                                                                                                                              | Denial-of-service attacks are illegal and carry a maximum penalty of 10 years in prison under the Computer Misuse Act 1990 + amendments.                                                                                                               |
| **Denial of Service (DoS)**                  | A class of attacks focused on compromising the availability of a service by breaking it or by overloading/starving it of resources.                                                                                                    | Techniques include the Ping of Death (sending malformed packets) or Permanent DoS (replacing firmware with non-functional firmware).                                                                                                                   |
| **Distributed Denial of Service (DDoS)**     | A popular form of DoS attack where many, distributed willing or unwilling participants contact the victim, frequently carried out using botnets.                                                                                       | In 2016, the Mirai botnet set DDoS bandwidth records by using 145,000 webcams (IoT devices) to exceed 1 Tbit/s attacks.                                                                                                                                |
| **Botnets**                                  | Networks of compromised machines (bots) used in DDoS attacks; they are built by exploiting widespread vulnerabilities, installing code, and instructing the bots to request a service from the victim.                                 | Early botnets consisted of Windows PCs, but nowadays frequently involve Internet of Things (IoT) devices like DVRs, WiFi routers, and Internet cameras.                                                                                                |
| **Social Engineering**                       | The act of "hacking people," often done via email (phishing), over the phone, or in person to obtain passwords, information, or install malware.                                                                                       | Hackers stole a password from an IT administrator after sympathetic employees allegedly let them into the building during the 2014 Sony Attacks.                                                                                                       |
| **Injection Attack**                         | A security flaw that occurs when malicious data is sent to an interpreter as part of a command or a query.                                                                                                                             | Examples include SQL injection, OS injection, and LDAP injection. All forms of user input (SQL queries, forms, data uploads) can make an application vulnerable.                                                                                       |
| **SQL Injection**                            | An attack where SQL code is inserted or appended into application/user input parameters that are later passed to a back-end SQL server for parsing and execution. This attack breaches confidentiality and integrity.                  | Can be used to steal contents of databases (passwords, user data), modify data (e.g., delete all contents), or get unauthorized access to resources. A common example is using the string `‘or’ 1=1` in an input field to bypass authentication logic. |
| **Cross-site Scripting (XSS)**               | A type of injection attack in which malicious scripts are injected into trusted websites, and the malicious script is subsequently executed in the victim’s browser.                                                                   | Attackers can steal information (cookies, credentials), install key loggers, spy on the user, or modify webpage contents to perform phishing. The browser executes malicious injected code.                                                            |
| **Reflected Server XSS**                     | Occurs when malicious user input is received by the target server and then sent back to the browser (e.g., as an error or confirmation message) without that data being made safe to render.                                           | Example: A URL containing a script that the server echoes back, such as `http://yoursite.com/?q=<script>…`.                                                                                                                                            |
| **Stored Server XSS**                        | Considered the classic XSS attack type where malicious user input is permanently stored on the target server (e.g., in a database or message forum), and the client receives the stored data without it being made safe for rendering. | An attacker might leave a comment containing an attack script in a blog's comment section; every user reading that comment executes the script in their browser.                                                                                       |
| **Cross-site Request Forgery (CSRF/XSRF)**   | An attack where the attacker places a link or script on a web page that, when activated by the user, causes the browser to send a fraudulent request to the server to perform an unwanted action.                                      | The server receives a malicious request from the browser and acts on it. The goal is typically to cause a state change (e.g., transferring money to an attacker's account).                                                                            |
| **Active Data Uploads**                      | A vulnerability created when a site allows data to be uploaded (e.g., image files), and an attacker uploads an active executable file (e.g., a `.php` file) and then runs it remotely.                                                 | Can be mitigated by putting uploads outside of the path to the document root, preventing direct access and execution.                                                                                                                                  |
| **Buffer Overflows (or Overruns)**           | Occur when applications do not properly account for the size of input data, causing excess data to be written over other areas in memory used by other applications or the operating system.                                           | Proper **bounds checking**—setting a limit on the amount of data accepted—can nullify this type of attack.                                                                                                                                             |
| **Race Conditions**                          | Occur when multiple processes share access to a resource, and the correct operation depends on the precise ordering or timing of transactions, leading to potentially undesirable results.                                             | If two users attempt to withdraw money from the same account simultaneously without proper handling, the final balance recorded may be incorrect.                                                                                                      |
| **Format String Attack**                     | A type of input validation problem where certain print functions in languages like C or C++ can be exploited using formatting parameters (e.g., `%n`) to manipulate or view the internal memory of an application.                     | An attacker might write a particular value into a location in memory, potentially crashing the application or forcing the operating system to run a command.                                                                                           |
| **Principle of Least Privilege**             | The security principle that mandates allowing the minimum permissions required for both users and the internal activities of software.                                                                                                 | Limits the potential damage if an account is compromised, ensuring that a user who gains access to restricted application portions cannot proceed.                                                                                                     |
| **Clickjacking**                             | An attack that exploits the browser's graphical display capabilities to trick a user into clicking something they did not intend, usually by placing an invisible layer over the actual content.                                       | An attacker might hide a "buy now" button under a seemingly innocuous button like "more information".                                                                                                                                                  |
| **Fuzz Testing / Fuzzers**                   | A process (Fuzz testing) where specialized tools (Fuzzers) bombard applications with all manner of unexpected data and inputs to discover completely unknown or unexpected problems.                                                   | Used to discover vulnerabilities in both existing software and software currently in development.                                                                                                                                                      |
| **Nikto / Wikto**                            | Nikto is a free, open source, command-line Web server analysis tool; Wikto is a Windows version of Nikto that provides a graphical user interface (GUI).                                                                               | These tools perform checks for common vulnerabilities and index (spider) all visible files and directories on the target server.                                                                                                                       |
| **White-lists / Black-lists**                | **White-lists** identify safe tokens and allow only those. **Black-lists** identify unsafe tokens and attempt to filter those out.                                                                                                     | **White-lists** are generally recommended over black-lists for input validation because it is impossible to list every unacceptable character that could cause a problem.                                                                              |
| **Responsible Disclosure**                   | A process where a security researcher contacts the vendor or authority first, waits for security updates, and then performs public disclosure (description of vulnerability without exploit code).                                     | Some researchers follow a policy of publicly disclosing vulnerabilities after a fixed period if the vendor is unresponsive, even if an update is not ready.                                                                                            |
# SQL Injection (Server-Side Attack)
### When does an SQL injection occur?
A **SQL Injection** vulnerability occurs when an application developer fails to adequately validate or encode user-supplied values that are intended to be data, allowing that input to be interpreted as code and concatenated directly into a database query string. SQL injection is a type of injection attack where malicious SQL code is inserted or appended into application/user input parameters, which are subsequently passed to a back-end SQL server for parsing and execution.

When user input is improperly handled and concatenated into a query string, the attacker can effectively change the logic and structure of the intended SQL query, causing the database to execute commands different from those expected by the developer. **SQL databases interpret the quote character (') as the boundary between code and data**. If an application fails to filter input for special characters such as the single quote (`'`), an attacker can terminate the string intended for data and inject their own SQL code.

### Example of Vulnerable SQL Query and Logic Alteration

Consider a vulnerable PHP script used for user login authentication, which dynamically creates a SQL statement by concatenating user input for `username` and `password`.

**1. The Original Vulnerable Query Structure (Code):**

A common, dynamically built SQL query for checking authentication might look like this:

`$query = "SELECT * FROM CMSSUsers WHERE username = '" . $user . "' AND password = '" . $password . "';"`

**2. The Intended Query (with normal input):**

If a legitimate user enters:

- `username`: `foo`
- `password`: `bar`

The resulting SQL statement executed by the database would be:

`SELECT userid FROM CMSUsers WHERE username = 'foo' AND password = 'bar'`

This query is intended to return zero or one record, allowing the application to check if the credentials are valid.

**3. The Injected Query (Bypassing Authentication):**

If an attacker inputs the following into the password field:

`' OR '1'='1`

And a benign value (like `'foo'`) into the username field, the resulting SQL statement executed by the database becomes:

`SELECT userid FROM CMSUsers WHERE username = 'foo' AND password = '' OR '1'='1'`

In this altered query, the input `'` (single quote) terminates the intended password string, and the `OR '1'='1'` condition is appended. Since the condition `1=1` is always true, the entire `WHERE` clause evaluates to **true** (the logic of the query is altered), regardless of the actual username or password entered. This attack causes the query to return all user IDs from the `CMSUsers` table, allowing the attacker to bypass the intended authentication logic and potentially gain unauthorized access.

If the application expects more than zero records back from this query to grant access, the injected string successfully fools the application into believing the correct authentication credentials were provided. SQL injection can be used to gain or escalate privileges within the database.

## Prepared Statements (Parameterized Queries) vs Input Sanitisation
**Prepared Statements (Parameterized Queries)** prevent SQL injection by ensuring a strict separation between code and data, which is the primary defense mechanism recommended against this vulnerability.

### Prepared Statements and Prevention of SQL Injection

The core defense against SQL injection is to **separate code and data**. Prepared statements, also referred to as parameterized queries, achieve this by utilizing a "template" statement.

1. **Template Creation:** A structured query template is created first, defining the SQL command with placeholders for where data input will eventually go.
2. **Data Insertion:** The user-supplied values are then inserted into the template's placeholders _only_ as data.
3. **No Code Interpretation:** Because the data is sent to the database separate from the query template, the database engine processes the user input strictly as literal data values, regardless of whether it contains special SQL characters, such as the single quote (`'`), which databases usually interpret as the boundary between code and data. This guarantees that an attacker cannot alter the logical structure of the SQL statement by inserting executable code.

If an attacker tries to pass SQL code through a prepared statement, the database will treat the entire input, including any malicious commands or characters, as a single, harmless string of data to be matched against a database field, rather than as executable instructions.

### Contrast with Input Sanitization (Input Validation)

**Input Sanitization** (or Input Validation) is a defense mechanism that involves checking the input taken into an application and filtering it for unexpected or undesirable content, such as special characters like `%`, `'`, `;`, and `/`.

- **Goal of Sanitization:** The goal of input validation is to filter user input so that the application prevents the browser or server from interpreting it as code. For instance, in the case of a format string attack, careful input checking can remove offending characters or put error handling in place.
- **Methodology:** This defense relies on identifying "unsafe tokens" and attempting to filter them out (**black-lists**), or, preferably, identifying only "safe tokens" and allowing only those (**white-lists**).

### Primary Defense: Prepared Statements vs. Input Sanitization

**Prepared Statements are the primary defense against SQL injection**, while Input Sanitization is a good supplementary defense, particularly when used in the form of **white-listing**.

**Why Prepared Statements are Primary:**

- **Guaranteed Separation:** Prepared statements fundamentally address the root cause of SQL injection by ensuring that user input cannot be executed as code by the database, guaranteeing the separation of data and code.
- **Reliability:** This method is inherently more reliable because it places the protective mechanism in the structure of the database query itself, rather than relying on application code to constantly check every possible malicious input permutation.

**Why Input Sanitization/Validation is Secondary (or Less Reliable):**

- **Difficulty of Black-listing:** Input validation, especially when relying on black-lists, is problematic because it is impossible to list every unacceptable character or combination that could cause a problem. An attacker may find unexpected or undesirable content that a developer forgot to filter out.
- **White-listing is Preferred:** While black-listing is discouraged, the general principle of validating input remains a necessary defense. The sources recommend using **white-lists** of safe tokens instead of black-lists of unsafe tokens, as this is a more secure validation technique.

In summary, the fundamental general security countermeasure is to **separate data and code**. Since prepared statements achieve this separation directly within the database interaction, they are considered the primary defense for protecting against SQL injection attacks. Trying to sanitize or validate input is often difficult, as it is impossible to know every character or sequence an attacker might use to attempt compromise.

# XSS and CSRF
### Cross-Site Scripting (XSS) Definition

Cross-Site Scripting (XSS) is a type of injection attack in which **malicious scripts are injected into trusted websites**. When a victim views the affected web page or media, the malicious script is executed automatically in the victim’s browser. The client/victim's browser trusts the server and executes the malicious script that it receives from the server.

### Differences Between Reflected XSS and Stored XSS

The two main types of server-side XSS attacks are Reflected Server XSS and Stored Server XSS, distinguished primarily by where the malicious user input is stored and how it reaches the victim's browser.

|Feature|Reflected Server XSS|Stored Server XSS|
|:--|:--|:--|
|**Description**|Malicious user input is received by the target server and immediately sent back to the browser, typically as an error or confirmation message. The client receives the data without it being made safe to render.|Considered the **classic XSS attack type**. Malicious user input is **permanently stored on the target server** (e.g., in a database or message forum). The client receives the stored data from the server without it being made safe to render in the browser.|
|**Source/Saving Location**|The malicious script is typically **embedded in a link** or through a form provided by the attacker. For instance, the script might be part of a URL query string, like `http://yoursite.com/?q=<script>…`.|The malicious script is **saved on the target server** in a storage location, such as a database or a message forum. An attacker might leave a comment containing the attack script in a blog's comment section.|
|**Execution Context**|The script is only executed in the victim's browser if the victim clicks the specific link or accesses the crafted URL, causing the server to **reflect** the malicious input back.|The script is executed in the victim's browser every time they view the page that retrieves the stored malicious data.|

### Impact: Data an Attacker Can Steal Using XSS

When a malicious script is executed in the victim’s browser, the attacker can use the script to compromise the user’s session or machine. An attacker can steal information such as **cookies** and **credentials**, spy on the user (for example, by installing a **key logger**), or modify the webpage contents to perform **phishing attacks**.

Essentially, XSS allows the attacker to execute their own code (the malicious script) within the context of the trusted website, leveraging the browser's trust in the server.

## CSRF Attacks
The **Cross-Site Request Forgery (CSRF)** attack, also known as XSRF, is a mechanism that exploits the trust a server has in a user’s authenticated browser session to execute unwanted actions.

### Mechanism of a CSRF Attack

A CSRF attack typically proceeds through the following steps:

1. **User Authentication and Session:** The user/victim must first be authenticated to a legitimate server (e.g., a bank's website) and currently be in an active session with that server.
2. **Attacker Placement:** The attacker provides a script or a link with malicious side-effects on a separate web page (the attacker's website or an email). The attacker's goal is not to observe the outcome but to cause a **state change** on the victim's server.
3. **Victim Activation:** The user, while still logged in to the target server (e.g., MySpiffyBank.com), visits the attacker's malicious website (e.g., BadGuyAttackSite.com) or clicks on the malicious link.
4. **Fraudulent Request Sent:** The user’s browser interprets the content provided by the attacker and automatically causes the browser to send a fraudulent request to the legitimate server.
5. **Server Execution:** Because the request comes from the user’s own browser—which is already authenticated and in a session with the server—the server cannot distinguish between this malicious request and a genuine, desired request. Consequently, the server executes the client/victim’s request, performing the state change requested by the attacker.

### How the User's Browser is Tricked

The attacker tricks the user's browser by placing a link or links on a page that are designed to be automatically executed without the user's explicit knowledge or consent.

For example, if the attacker knows that a bank executes a money transfer via a specific URL structure, the attacker can embed that URL structure into their own website. When the victim visits the attacker's page, the malicious links or scripts execute in the background. This action causes the browser to send a request to the bank's server to perform an unwanted action, such as transferring money to the attacker's account or sending spam emails. The attack is successful if the user is simultaneously logged into the target site.

The key difference between XSS and CSRF is that in **CSRF, the server receives the malicious request from the browser and acts on it**, whereas in XSS, the browser executes the malicious injected code.

### Role of Cookies in CSRF Attacks (Session Management)

While the sources do not explicitly name "cookies," the function described in CSRF relies entirely on the existing **authenticated session** the user has with the target server. In modern web applications, **session cookies** are the primary mechanism used by browsers to maintain authentication status (i.e., proving the user is logged in).

When a user is authenticated and has an active session, the browser automatically includes the necessary session data (stored, often, in cookies) with every request made to that domain. Because the fraudulent request generated by the attacker's link is sent from the authenticated browser, the browser automatically attaches the authentication details, making the request appear legitimate to the target server. The server treats the malicious request as if the legitimate user voluntarily initiated the activity.


# Comparing Different Attack Types

|Attack Type| Target: Does it attack the Database/Server or the User/Browser?                                                                          | Mechanism: Does it inject code, inject SQL, or misuse a session?                                                                                                                                         | Primary Defense                                                                                                           |
|:--|:--|:--|:--|
|**SQL Injection (SQLi)**| Primarily attacks the **Database/Server**. An SQL injection attack is used to steal contents from databases or modify database contents. | **Injects SQL** code into application/user input parameters that are later passed to a back-end SQL server. It exploits the lack of separation between code and data by altering the logic of the query. | **Parameterized Queries** (or Prepared Statements), which ensure the separation of code and data.                         |
|**Cross-Site Scripting (XSS)**| Attacks the **User/Browser**. The **malicious script is executed in the victim’s browser**.                                              | **Injects code** (malicious scripts) into a trusted website, which the client's browser executes.                                                                                                        | Context-sensitive (server-side) **Output Encoding**, combined with Input Validation (using white-lists).                  |
|**Cross-Site Request Forgery (CSRF/XSRF)**| Attacks the **Server** (by making the server execute an unwanted action). The purpose is to cause a **state change** on the server.      | **Misuses a session** by tricking the authenticated browser into sending a fraudulent request to the server. The server receives the malicious request from the browser and acts on it.                  | Including **unpredictable tokens** in valid requests for critical state changes. (This method utilizes Anti-CSRF Tokens). |
# Exam Style Questions

#### Short Answer Questions (5)

**1. Question:** What is the maximum penalty specified by the Computer Misuse Act 1990 + amendments for carrying out a denial-of-service (DoS) attack, and why is "unauthorised hacking" or "testing" illegal? **Answer:** Denial-of-service attacks are illegal and carry a **maximum penalty of 10 years in prison**. "Unauthorised hacking/“testing”/attacking of computer systems is illegal".

**2. Question:** Differentiate between the primary goal of Cross-Site Scripting (XSS) and Cross-Site Request Forgery (CSRF) attacks regarding their interaction with the victim's browser and the target server. **Answer:** In **XSS**, the **browser executes malicious injected code**. In **CSRF**, the **server receives the malicious request from the browser and acts on it**, and the purpose of the attack is typically to cause a **state change** in the server.

**3. Question:** What is the recommended primary defense against SQL Injection attacks, and why is this method superior to using "black-lists" for input filtering? **Answer:** The recommended primary defense is to **Separate code and data** by using **prepared statements**. This approach is superior because it is impossible to list every unacceptable character that could cause a problem, making **black-lists** unreliable, whereas prepared statements fundamentally ensure that user input is treated only as data, not as executable code.

**4. Question:** Name and briefly define two types of denial-of-service (DoS) attacks that aim to "Break the service." **Answer:** Two types of DoS attacks that break the service are:

1. **Ping of death:** Sending a malformed (e.g., larger-than-expected) packet to crash the victim’s service.
2. **Permanent DoS (PDoS):** Exploiting a security flaw to replace a device’s firmware with non-functional firmware.

**5. Question:** What is a **buffer overflow** (or overrun) and what simple technique can nullify this type of attack entirely? **Answer:** Buffer overflows occur when applications do not properly account for the size of input data, causing excess data to be written over other areas in memory used by other applications or the operating system. This attack can be nullified entirely by implementing **proper bounds checking** (setting a limit on the amount of data accepted).

---

#### Scenario-based Long-form Questions (2)

**1. Scenario Question:** A popular online message forum allows users to post comments using a web form, and these comments are immediately saved and displayed to all other users. An attacker posts a comment that contains a malicious `<script>` tag instead of plain text.

1. Identify the type of injection attack being described, and explain the mechanism by which the malicious script is stored and executed.
2. What specific information might the attacker be able to steal using this technique, and what is the key defensive mechanism recommended for server-side code to mitigate this vulnerability?

**Answer:**

1. **Attack Identification and Mechanism:** The attack described is **Stored Server XSS** (Cross-Site Scripting). It is also referred to as the classic XSS attack type.
    
    - **Storage:** The attacker injects malicious user input (the `<script>` tag) via the comment form, and this input is **permanently stored on the target server** (e.g., in a database or message forum).
    - **Execution:** When another user visits the blog page, the **client receives the stored data from the server** without that data being made safe to render in the browser. The victim’s browser then executes the malicious script automatically because the client/victim’s browser trusts the server.
2. **Stolen Information and Defense:**
    
    - **Stolen Information:** If the malicious script executes in the victim’s browser, the attacker can steal information such as **cookies** or **credentials**, install a **key logger** to spy on the user, or modify the webpage contents to perform **phishing attacks**.
    - **Primary Defense:** The first line of defense against Server XSS is to use **context-sensitive (server-side) output encoding** with a secure encoding library. A good secondary defense is **Input Validation**, specifically using **white-lists of safe tokens** instead of black-lists of unsafe tokens, to filter user input so the browser does not interpret it as code.

**2. Scenario Question:** The 2011 Sony Attacks involved multiple attack vectors, including social engineering and physical access to systems, leading to the theft of personal and financial data from 77 million users.

1. Explain how **social engineering** and **physical access** facilitated the Sony breach, according to the sources.
2. Identify three specific Web Application Security Risks listed in the OWASP Top 10 (2013 or 2017 list) that were also cited as possible attack methods used against Sony.
3. Besides application vulnerabilities, what other security weakness was exploited in the TJX breach that allowed the attackers to initially compromise the local store network?

**Answer:**

1. **Social Engineering and Physical Access:**
    
    - **Social Engineering:** This involved "hacking people" via email (phishing), over the phone, or in person to obtain passwords or install malware. In the Sony case, hackers stole a **password from an IT administrator**.
    - **Physical Access:** Sympathetic employees allegedly **let hackers into the building**. Once on the network, the hackers planted malware which then found and stole other passwords.
2. **OWASP Top 10 Risks Cited in Sony Attacks:** The sources explicitly list several OWASP Top 10 risks used against Sony, including:
    
    - **A1 Injection**.
    - **A3 Cross Site Scripting (XSS)**.
    - **A8 Cross-Site Request Forgery (CSRF)**. _(Note: Broken Authentication and Session Management (A2 in 2013) was also cited as a vulnerability used, which led to password theft)_.
3. **TJX Breach Weakness (Non-Application):** The TJX breach began with an attack on the **wireless network** used to communicate between devices. The system used the 802.11b wireless protocol and **Wired Equivalent Privacy (WEP) encryption**, which was described as an **outdated encryption protocol with well-known weaknesses** and was rendered obsolete in 2002. Attackers later created their own accounts and accessed the stolen data because of the **lack of firewalls and encryption** on sensitive portions of the TJX network.