---
title: Week 01 - Introduction to Information and Network Security
date: 2025-12-13
tags:
  - risk-management
  - CIA-triad
  - OWASP
  - definitions
aliases:
  - CIA Triad
  - Risk Assessment
  - Threat Modeling
summary: The core relationships between Threat, Vulnerability, and Risk, plus the OWASP rating methodology.
---
## Key Terms 

| Term                               | Definition                                                                                                                                           | Exam Context/Example                                                                                                                                                                           |
| :--------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Information Security**           | Protecting information and information systems from unauthorized access, use, disclosure, disruption, modification, or destruction.                  | The goal is to protect data (wherever it is) and system assets from misuse.                                                                                                                    |
| **Risk**                           | The possibility to suffer harm or loss. It is also defined as a function of loss associated with an event and the probability that the event occurs. | Risk exists only when there is a **threat** and a **vulnerability** that the specific threat can exploit.                                                                                      |
| **Threat**                         | Potential cause of an unwanted event that may harm assets. Something that has the potential to cause us harm.                                        | An earthquake hazard. A specific virus may pose a threat to a Windows operating system but not a Linux operating system.                                                                       |
| **Vulnerability**                  | A characteristic of a system that can be exploited by a threat. Weaknesses or holes that can be used by threats to cause harm.                       | Running a specific operating system or application. A structure made from wood when facing a fire threat.                                                                                      |
| **Impact**                         | An additional factor added to the threat/vulnerability/risk equation, relating to the value of the asset being threatened.                           | If unencrypted backup tapes contain only cookie recipes, the impact is low, potentially resulting in no risk.                                                                                  |
| **Countermeasure**                 | Means to detect, deter, or deny attacks to threatened assets.                                                                                        | These are deployed to reduce risk. They are evaluated based on how well they reduce risk, their expense, and new risks they bring.                                                             |
| **Controls**                       | Measures put in place to help ensure a given type of threat is accounted for, used to mitigate risks.                                                | Controls are divided into three categories: physical, logical, and administrative.                                                                                                             |
| **Physical Control**               | Controls that protect the physical environment where systems sit or data is stored, and control access in and out of such environments.              | Fences, locks, bollards, guards, cameras, fire suppression systems, and backup power generators.                                                                                               |
| **Logical/Technical Control**      | Controls that protect the systems, networks, and environments that process, transmit, and store data.                                                | Passwords, encryption, firewalls, intrusion detection systems, and logical access controls.                                                                                                    |
| **Administrative Control**         | Controls based on rules, laws, policies, procedures, and guidelines that set out how users are expected to behave.                                   | A policy requiring a password change every 90 days.                                                                                                                                            |
| **Defense in Depth**               | A strategy to formulate a **multilayered defense** that allows for successful defense should one or more defensive measures fail.                    | Placing defenses at the external network, internal network, host, application, and data layers. The goal is to delay an attacker long enough to detect the attack and mount an active defense. |
| **CIA Triad**                      | A model used as a foundation for discussing security, composed of Confidentiality, Integrity, and Availability.                                      | This model is very focused on security as it pertains to data.                                                                                                                                 |
| **Confidentiality**                | The ability to protect our data from those who are not authorized to view it.                                                                        | Maintaining the confidentiality of a Personal Identification Number (PIN) while withdrawing money from an ATM. Compromised by unauthorized viewing or penetration of systems.                  |
| **Integrity**                      | The ability to prevent data from being changed in an unauthorized or undesirable manner.                                                             | Mechanisms like permissions in Windows and Linux file systems allow control over changes. If medical test data were altered, integrity would be lost.                                          |
| **Availability**                   | The ability to access our data when we need it.                                                                                                      | Loss can result from power loss, application problems, network attacks, or a Denial of Service (DoS) attack.                                                                                   |
| **Denial of Service (DoS) Attack** | Loss of availability caused by an outside party, such as an attacker.                                                                                | A DoS attack on a mail server.                                                                                                                                                                 |
| **Parkerian Hexad**                | A more complex variation of the CIA triad, consisting of Confidentiality, Integrity, Availability, Possession or Control, Authenticity, and Utility. | It provides a more extensive model for describing security situations than the CIA triad alone.                                                                                                |
| **Possession or Control**          | Refers to the physical disposition of the media on which the data is stored.                                                                         | Losing a shipment of encrypted backup tapes is a possession problem, even if the data itself remains confidential.                                                                             |
| **Authenticity**                   | Allows discussion about the proper attribution as to the owner or creator of the data in question.                                                   | Violating authenticity occurs if an e-mail message is altered to appear to come from a different e-mail address.                                                                               |
| **Utility**                        | Refers to how useful the data is to us.                                                                                                              | Encrypted tapes would likely be of very little utility to an unauthorized person, whereas unencrypted tapes would be of much greater utility.                                                  |
| **Nonrepudiation**                 | Prevents someone from taking an action (e.g. sending an e-mail) and then later denying that he or she has done so.                                   | This concept is critical to e-commerce and can be enforced through mechanisms like digital signatures.                                                                                         |
| **Interception (Attack)**          | Attacks that allow unauthorized users to access data, applications, or environments.                                                                 | Eavesdropping on phone conversations or unauthorized file viewing/copying. Primarily attacks confidentiality.                                                                                  |
| **Interruption (Attack)**          | Attacks that cause assets to become unusable or unavailable for use, on a temporary or permanent basis.                                              | A DoS attack on a mail server, which affects availability.                                                                                                                                     |
| **Modification (Attack)**          | Attacks that involve tampering with an asset.                                                                                                        | Altering the contents of a configuration file for a Web server. Primarily an integrity attack.                                                                                                 |
| **Fabrication (Attack)**           | Attacks that involve generating data, processes, communications, or other similar activities with a system.                                          | Generating spurious information in a database or spoofing an email. Primarily affects integrity.                                                                                               |

--- 
### Relationship Between Threat, Vulnerability, and Risk
The relationship between **Threat, Vulnerability, and Risk** is fundamental to security risk assessment, as risk is only present when a threat can exploit a vulnerability.

1. **Threat:** A threat is defined as the **potential cause of an unwanted event that may harm assets**. In the context of information security, a threat is something that has the potential to cause harm. Examples of threats include malicious actors such as organised criminals or nation states, or even natural disasters.
2. **Vulnerability:** A vulnerability is a **characteristic of a system that can be exploited by a threat**. Essentially, vulnerabilities are weaknesses, or holes, that a threat can use to cause harm. An example of a vulnerability is running a specific operating system or application, or using a data center populated beyond the capacity of its air-conditioning system.
3. **Risk:** Risk is the **possibility to suffer harm or loss**. It represents the likelihood that something bad will happen.

**The Key Relationship:**

Risk exists only when there is a coincidence of both a threat and a vulnerability that the specific threat can exploit. If a threat is present but there is no corresponding vulnerability, there is no credible risk. For example, a fire (threat) poses a risk if the structure is made of wood (vulnerability), but if the structure is concrete, the credible risk is eliminated or greatly reduced.

Risk itself is described as a function of the loss associated with an event and the probability that the event occurs. Threats lead to risk, and threats exploit vulnerabilities, which increases risk.

### OWASP Risk Rating Methodology Formula

The OWASP Risk Rating Methodology is one resource used for risk assessment. When assessing risk resulting from a vulnerability and its exploit, the sources define risk in terms of impact and probability/likelihood.

The general relationship or working definition for **risk associated with vulnerabilities** presented in the sources is:

$$ \text{risk} = (\text{impact to asset from exploit of vulnerability}) \text{ x } (\text{probability of occurrence}) $$

This aligns with the general components illustrated in the OWASP approach, which evaluates risk based on **Impact** and **Likelihood**. Although measuring the probability of occurrence and impact can be difficult, this formula outlines the fundamental assessment needed for risk.


## Dealing with Risk
The four main ways of dealing with risk are Accept, Transfer, Mitigate, and Avoid. These methods represent alternative options for managing risk, which is the possibility of suffering harm or loss.

Here is a summary of each method and a practical business example:

|Risk Handling Strategy|Summary Description|Practical Business Example|
|:--|:--|:--|
|**Accept**|Choosing to **accept the risk** means that an organization acknowledges the existence of the risk but decides not to implement countermeasures or defenses against it, often because the potential loss is small or the cost of mitigation is too high.|A small business might accept the risk of having a non-redundant database back-end for their payment processing system if the cost of downtime is calculated to be lower than the cost of building and maintaining a redundant system.|
|**Transfer**|**Transferring the risk** involves shifting the financial consequences of a potential loss to a third party. This is a common strategy when dealing with risks that are expensive or catastrophic if they occur.|A company buys an **insurance** policy, such as a bankers' blanket bond or cyber-insurance, to cover the financial losses resulting from fraud, employee dishonesty, or cyber incidents.|
|**Mitigate**|**Mitigating the risk** involves taking steps or implementing measures, called **countermeasures** or **controls**, to actively reduce the probability of the threat exploiting the vulnerability, or to reduce the potential impact/loss. Mitigation involves prioritizing risks, identifying appropriate defenses, evaluating how well they reduce risk versus their cost, and then implementing them.|An organization mitigates the risk of a system going down due to a DoS attack (Interruption) by installing redundant hardware (availability control) or implementing a multilayered defensive strategy called **Defense in Depth**.|
|**Avoid**|**Avoiding the risk** involves taking action to eliminate the risk entirely by removing either the threat or the vulnerability. By removing the asset, eliminating the threat, or taking steps so the organization is no longer exposed, the risk is eliminated.|To avoid the risk of data loss from earthquakes, a company might choose to **live where there are no earthquakes** or move their data center to a geographically stable location. Similarly, avoiding the risk of exposure to a known virus could mean discontinuing the use of a specific operating system that the virus targets.|

Risk is assessed using the relationship: $\text{risk} = (\text{impact to asset from exploit of vulnerability}) \text{ x } (\text{probability of occurrence})$. When managing risk, organizations aim to minimize the risk and deploy countermeasures to reduce it.

--- 
# Exam Style Questions

### Short Answer Exam Questions

**1. Question:** Define a **Vulnerability** and provide a real-world example of a vulnerability that is exploited by the threat of fire, as discussed in the sources.

**Answer:** A vulnerability is defined as a **characteristic of a system that can be exploited by a threat**. In essence, vulnerabilities are weaknesses or holes that can be used by threats to cause harm. Regarding the threat of fire, a vulnerability that matches this threat is a **structure made from wood**. If the structure were made of concrete, the credible risk would be eliminated or greatly reduced.

**2. Question:** According to the provided material, what is the working definition or specific formula used for assessing **risk associated with vulnerabilities**, and what two primary factors determine this outcome?

**Answer:** The working definition for risk associated with vulnerabilities is expressed as a multiplication of two factors: $$\text{risk} = (\text{impact to asset from exploit of vulnerability}) \text{ x } (\text{probability of occurrence})$$. The two primary factors are the **impact to the asset from the exploit of the vulnerability** and the **probability of occurrence**.

**3. Question:** When managing risks, controls are measures put in place to help mitigate threats. Name and briefly describe the three categories into which controls are divided.

**Answer:** The three categories of controls are:

1. **Physical Controls:** These protect the physical environment where systems sit or data is stored, and they control access in and out of such environments. Examples include fences, locks, guards, and fire suppression systems.
2. **Logical/Technical Controls:** These protect the systems, networks, and environments that process, transmit, and store data. Examples include passwords, encryption, firewalls, and intrusion detection systems.
3. **Administrative Controls:** These are based on "paper" items like rules, laws, policies, procedures, and guidelines, setting out how users are expected to behave. An example is a policy requiring password changes every 90 days.

**4. Question:** Name the three additional principles that expand the classical CIA triad (Confidentiality, Integrity, Availability) into the **Parkerian Hexad** model.

**Answer:** The three additional principles that, along with Confidentiality, Integrity, and Availability, make up the Parkerian Hexad are: **Possession or Control**, **Authenticity**, and **Utility**.

**5. Question:** Give two distinct strategies for dealing with risk mentioned in the sources that allow an organization to eliminate the risk entirely or shift the financial consequences of the risk to a third party.

**Answer:**

1. **Avoid the risk:** This strategy eliminates the risk entirely by removing the exposure, such as deciding to live where there are no earthquakes, or discontinuing the use of a specific operating system targeted by a virus.
2. **Transfer the risk:** This strategy shifts the financial consequences of a potential loss to a third party, typically by purchasing **Insurance**.

---

### Scenario-Based Long-Form Questions

**1. Question:** A major financial institution determines that its highly sensitive long-term customer key encryption database is backed up daily onto unencrypted magnetic tapes. These tapes are hand-carried off-site by a courier for storage. Using the Risk Assessment process outlined in the sources, detail the three main steps that must be taken to analyze this situation. Additionally, explain how two principles of the **Parkerian Hexad** are affected if the tapes are stolen during transport, and propose a mitigation control to address the risk.

**Answer:** The **Risk Assessment** process outlined involves three main steps:

1. **Identify assets, threat agents, and threats to assets:** This step requires determining what needs protection (the sensitive encryption database and the keys), who the potential attackers are (threat agents, e.g. organised criminals or insiders), and what the unwanted event is (e.g. unauthorized access or theft).
2. **Identify vulnerabilities that can be exploited:** This involves finding weaknesses, such as the fact that the backup tapes are unencrypted and are transported physically, which can be exploited by the threat.
3. **Measure probability of occurrence and impact (potential loss) of exploits:** The probability of occurrence (e.g. theft during transit) must be measured, alongside the impact (potential loss), which would be severe since the asset holds highly sensitive customer keys.

If the unencrypted tapes are stolen, the following **Parkerian Hexad** principles are affected:

- **Confidentiality:** This principle is violated because the data on the tapes is unencrypted and unprotected from those unauthorized to view it. Since the data is sensitive customer keys, this represents a major breach of confidentiality.
- **Possession or Control:** This principle refers to the physical disposition of the media. Losing the shipment means the company has lost physical control or possession of the media, even before considering the data's confidentiality status.
- **Utility (Likely Impact):** If the data were readable (unencrypted), it would be of great utility to an unauthorized person.

To **Mitigate** the risk of theft and data exposure, the organization must implement appropriate countermeasures. A critical logical control measure would be to **mandate encryption** of all sensitive data backup media, ensuring that if possession is lost, confidentiality is maintained (e.g. making the data of very little utility to the unauthorized person).

**2. Question:** A highly motivated competitor attempts to access your confidential source code database by exploiting a known bug in the database software, which would allow them to unauthorizedly read or copy the files. Identify the primary **CIA Triad** security property being attacked, and specify which of the four **attack categories** this action falls under. Finally, explain the purpose of the **Defense in Depth** strategy in managing this type of malicious activity.

**Answer:** The primary security property being attacked is **Confidentiality**. Confidentiality is the ability to protect data from those who are not authorized to view it, and the unauthorized reading or copying of source code directly violates this principle.

This action falls into the **Interception** attack category. Interception attacks primarily target confidentiality by allowing unauthorized users to access data or applications, taking the form of unauthorized file viewing or copying.

The purpose of the **Defense in Depth** strategy in managing this malicious activity is to formulate a **multilayered defense** that allows for a successful defense even if one or more defensive measures fail. The goal is **not** to keep the attacker out permanently, but to **delay the attacker long enough** to notice that an attack is in progress and buy enough time to take active measures to prevent the attack from succeeding. For a source code database, this might involve defenses at multiple layers, such as:

1. **Network perimeter controls** (e.g. firewalls, IDS) to slow the initial intrusion.
2. **Host-level controls** (e.g. anti-virus, authentication) on the server itself.
3. **Data-level controls** (e.g. encryption or access controls) on the source code files, ensuring that even if the host is compromised, the data remains protected.
### Steganography and Encryption

**Steganography** is defined as the practice of concealing information within another message or physical object in order to avoid detection. It can be used to hide virtually any type of digital content, including text, image, video, or audio content, and the hidden data is extracted at its destination. The term comes from the Greek words meaning 'hidden or covered' and 'writing'. In cybersecurity, threat actors frequently use steganography to conceal malicious tools, hide data, or send instructions for command-and-control servers within innocuous-seeming digital media files,.

The primary goal of both steganography and cryptography (of which encryption is a form) is to protect a message or information from third parties, but they use different mechanisms to achieve this.

**Distinction from Encryption:**

|Feature|Steganography|Encryption (Cryptography)|
|:--|:--|:--|
|**Primary Goal**|**Conceals the existence** of the message.|**Changes the format** of the message.|
|**Mechanism**|Hides the secret information inside a cover medium (e.g., embedding data in the least significant bits of an image file),,.|Changes the readable information into **ciphertext**, which can only be understood with a decryption key.|
|**Detection**|Does not change the format of the information and works by **avoiding suspicion**, making it difficult to detect, although it can sometimes be detected through "steganalysis",.|The resulting ciphertext is **easily visible** (it looks scrambled), meaning anyone intercepting the message can easily see that some form of encryption has been applied.|
|**Usage Context**|Steganography is sometimes used in conjunction with encryption, where the concealed content is first encrypted before being hidden. Encryption itself is a **logical control** used to protect data and enforce security principles like **confidentiality**,. Encrypted data is considered to have **very little utility** to an unauthorized person, unlike unencrypted data,.|

---

### Information Security vs. Cybersecurity

The sources provide a specific legal definition for **Information Security** but do not formally define or distinguish **Cybersecurity** in the introductory material.

#### Information Security

**Information Security** is defined by US law as: **“protecting information and information systems from unauthorized access, use, disclosure, disruption, modification, or destruction”**.

The fundamental goal of Information Security is to protect data, wherever it resides, and system assets from those who would seek to misuse them. This concept has become deeply embedded in many aspects of modern society due to the widespread adoption of computing technology,.

#### Cybersecurity

The sources use the term "cyber" in contexts like "cyber attacks",, "cybersecurity perspective", and "cybersecurity training", but they **do not provide an explicit definition for Cybersecurity** or explain how it differs from Information Security.