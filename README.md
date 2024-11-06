---
description: A software AVA_VAN.3 method for Linux-based TOEs
---

# README

_Disclaimer:

This set of documents and resources are a work in progress, and will likely always be only that. It is mainly built as I am learning pentesting, coming from less technical parts of CC. It is updated without a formal review process, as a part of the learning process itself.

For this reason, it should **not** be considered an authoritative resource: it is neither complete, nor error-free. It should rather be used as a companion document for evaluators trying to build their own method, and should be questioned at each step!

The method also assumes that the reader has some working knowledge of the CC AVA\_VAN.3 requirement, which implies the knowledge of the associated jargon: attack potential, TOE, TSF, and so on._

## Why this method

When performing product evaluation following Common Criteria (or ISO/IEC 15408/18045, which we will later call CC), one will have to perform vulnerability analysis (a.k.a. AVA\_VAN). The standard gives some expectations of which activities have to be performed (spoiler alert: _penetration testing_ is expected) and it also provides a scale of increasing effort that will result in increasing assurance in the product resistance. However, it remains a technology-agnostic standard, and does not really got into any depth wrt actual testing methods, tools or state-of-the-art.

On the other end, there are online and paper resources, as well as professional training and CTF competitions, related to penetration testing. Unfortunately, it is not always trivial to adapt this body of knowledge to CC evaluation, for several reasons:

 - it is non trivial to map a given tool or technique to a CC "attack potential";
 - penetration testing / CTF often addresses live systems populated with user data, rather than out-of-the-box products, which makes attack paths sometimes irrelevant in the context of a CC evaluation.
 - penetration testing / CTF frequently focus on the exploit, or at least the proof-of-concept, when CC focuses on identifying a vulnerability and being able to measure its gravity and exploitability: performing a PoC is an unnecessary cost during an evaluation
 - last, but not least, CC focuses on gray-box and white-box testing, allowing for lots of shortcuts compared to a "real" (read: "black-box") pentest

This set of documents and resources intends to help an evaluator in the course of performing a vulnerability analysis in the context of a **software CC evaluation at the level AVA\_VAN.3**. This makes it somehow relevant as well for standards such as FitCEM/CSPN/BSZ, that are meant as simplified versions of this standard at this specific level.

## Evaluation prerequisites
The [Prerequisites](Linux\_pentest/0\_Prerequisites.md) refine the CC requirements  in order to ensure that the information given in the ADV\_ and ALC\_ activities is ultimately relevant for the subsequent AVA\_VAN activities.


*Rationale:*
The main principle to understand is that **a product AVA\_VAN evaluation is not a CTF, it is not even pentesting** ! An evaluator that spends only 2 weeks of pentests is supposed to conclude whether it will resist 2 months of analysis in a black-box setting by an attacker with a similar skillset (see \[CEM, B.4.2.3 Calculation of attack potential]). To be able to make such a claim, the evaluator _must_ leverage more information (and access) than this hypothetical  attacker would possess:&#x20;

 - The evaluator _must_ participate in the ADV review! &#x20;
 - The evaluator is in a **white box** situation, and will often have a **privileged account** on the TOE to be tested. This is partly true even in a BSZ/CSPN evaluation: even if source code is not available, a privileged access to the TOE is provided.
 - Not only this, but the evaluator is in a **chosen white box**, in the sense that they can ask clarification/edits to the documentation as they see fit (within the limits of the CC requirements)
 - The analysis relies on the scoring of attacks on an attack potential scale, which means that the evaluator **does not have to actually perform attacks** whenever a vulnerability is scored as low enough.

In theory, CC requires such documentation and access, but the standard expresses this in a technology-agnostic manner - this often results in a documentation that mindlessly tries to meet CC requirements, without contextualizing/tailoring it for the specific TOE (or even TOE type). It ultimately gives the evaluator few actionable insight over a standard black-box context.


## Evaluation methodology

This method aims at providing a **limited set of choices for the evalautor**, so that they do not get lost during their assessment. The following methods are available:

 - [Linux system pentesting](Linux\_pentest/1\_Linux\_system\_pentesting.md) is a general method for pentesting applicative TOEs that run on Linux, or full systems based on a Linux OS
 - Supporting methods:
   - [Additional network methods](Linux_pentest/2_Additional_network_methods.md)
   - Code review:
     - [C code review](Linux\_pentest/Code\_review/C\_code\_review\_VAN3.md)
     - Python code review \[planned but not started yet]
   - [Public vulnerability analysis](\_1\_Public\_vulnerability\_analysis/Public\_vulnerability\_analysis\_101.md) \[planned but not started yet]

*Rationale:*
From a methodological point of view, the main issues are:

 - As in pentesting, if you act without a clear goal, you will probably not find anything in a constraint time frame. Apply "hack tricks" in various directions, without even being sure that they are actually relevant for the TOE security problem definition, will lead to nothing.
 - As you have many paths to assess a vulnerability, you need to use the fastest one. Some tools of the trade are also useless (e.g direct password attack is useless because you have a direct access to the passwors policy. Here you should simply give an expert opinion on the policy itself)

Therefore, the evaluator always needs to ask themselves at each step:

 - What am I trying to achieve? (i.e. what are my objectives and _attack scenarios_?)
 - What are the resources I can use? (i.e. what are the available _attack vectors_)
 - What can I use to exploit these resources? (_method and tools_)

