---
description: A software AVA_VAN.3 method for Linux-based TOEs
---
# Main table of contents
 - [Introduction and prerequisites](#introduction-and-prerequisites)
 - [Evaluation methodology](#evaluation-methodology)
 - [Why this method](#why-this-method)


# Introduction and prerequisites

This method is intended for evaluators performing Common Criteria AVA_VAN.3 evaluations of Linux-based software TOEs. This makes it somehow relevant as well for standards such as FitCEM/CSPN/BSZ, that are meant as simplified versions of this standard at this specific level.

This method defines [Prerequisites](Linux_pentest/0_Prerequisites.md). These prerequisites refine the Common Criteria ALC/ADV requirements for Linux-based TOEs. The AVA_VAN evaluator *must* participate in the ALC/ADV review and make sure that these prerequisites are met.


# Evaluation methodology

This method aims at providing a limited set of choices for the evaluator, so that they do not get lost during their assessment. The following methods are available:

 - [Linux system pentesting](Linux_pentest/1_Linux_system_pentesting.md) is a general method for pentesting applicative TOEs that run on Linux, or full systems based on a Linux OS
 - Supporting methods:
   - [Additional network methods](Linux_pentest/2_Additional_network_methods.md)
   - Code review:
     - [C code review](Linux_pentest/Code_review/C_code_review_VAN3.md)
     - Python code review \[planned but not started yet]
   - Public vulnerability analysis \[planned but not started yet]

# Why this method

When performing product evaluation following Common Criteria (or ISO/IEC 15408/18045, which we will later call CC), one will have to perform vulnerability analysis (a.k.a. AVA_VAN). The standard gives some expectations of which activities have to be performed (spoiler alert: _penetration testing_ is expected) and it also provides a scale of increasing effort that will result in increasing assurance in the product resistance. However, it remains a technology-agnostic standard, and does not really got into any depth wrt actual testing methods, tools or state-of-the-art. On the other end, there are online and paper resources, as well as professional training and CTF competitions, related to penetration testing. Unfortunately, it is not always trivial to adapt this body of knowledge to CC evaluation, for several reasons:

 - it is non trivial to map a given tool or technique to a CC "attack potential";
 - penetration testing / CTF often addresses live systems populated with user data, rather than out-of-the-box products, which makes attack paths sometimes irrelevant in the context of a CC evaluation.
 - penetration testing / CTF frequently focus on the exploit, or at least the proof-of-concept, when CC focuses on identifying a vulnerability and being able to measure its gravity and exploitability: performing a PoC is an unnecessary cost during an evaluation
 - last, but not least, CC focuses on gray-box and white-box testing, allowing for lots of shortcuts compared to a "real" (read: "black-box") pentest

Why are there prerequisites?

**A product AVA_VAN evaluation is not a CTF, it is not even real pentesting!** An evaluator that spends only 2 weeks of pentests is supposed to conclude whether it will resist 2 months of analysis in a black-box setting by an attacker with a similar skillset (see \[CEM, B.4.2.3 Calculation of attack potential]). To be able to make such a claim, the evaluator _must_ leverage more information (and access) than this hypothetical  attacker would possess:
 - The evaluator is in a **chosen white box** situation: **privileged account** on the TOE, possibility to ask clarification/edits to the documentation, etc.
 - The analysis relies on the scoring of attacks on an attack potential scale, which means that the evaluator **does not have to actually perform attacks** whenever a vulnerability is scored as low enough.


_Disclaimers:_

_This set of documents and resources are a work in progress, and will likely always be only that. It is mainly built as I am learning pentesting, coming from less technical parts of CC. It is updated without a formal review process, as a part of the learning process itself. For this reason, it should **not** be considered an authoritative resource: it is neither complete, nor error-free - I'm also well aware that parts of it are still naive drafts (e.g. the identificaiton scripts). So in a nutshell: use it as a companion document when building your own method, question it at each step, and if you can improve it, please [contact me](mailto:enhancedbasic@gmail.com) and contribute... The method also assumes that the reader has some working knowledge of the CC AVA_VAN.3 requirement, which implies the knowledge of the associated jargon: attack potential, TOE, TSF, and so on._

_I have been (and still am) working for various private or public organizations that have their own (sometime competing) interests in CC evaluation or certification. However, this repository is a personal project meant as a return of experience that could prove valuable for me OR anyone involved in such processes. It does not support the respective agendas of any of my past or current employers, and only tries to provide a reasonable, balanced and usable implementation of CC requirements for some technologies._
