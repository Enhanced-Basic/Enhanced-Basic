# What is a _SW pentesting method_ for _Enhanced-Basic attack potential_ ?

When performing product evaluation following Common Criteria (or ISO/IEC 15408/18045, which we will later call CC), one will have to perform vulnerability analysis (a.k.a. AVA_VAN). The standard gives some expectations of which activities have to be performed (spoiler alert: *penetration testing* is expected) and it also provides a scale of increasing effort that will result in increasing assurance in the product resistance. However, it remains a technology-agnostic standard, and does not really got into any depth wrt actual testing methods, tools or state-of-the-art.

On the other end, there are online and paper resources, as well as professional training and CTF competitions, related to penetration testing. Unfortunately, it is not always trivial to adapt this body of knowledge to CC evaluation, for several reasons:
 - it is non trivial to map a given tool or technique to a CC "attack potential";
 - penetration testing / CTF often addresses live systems populated with user data, rather than out-of-the-box products, which makes attack paths sometimes irrelevant in the context of a CC evaluation. 
 - penetration testing / CTF frequently focus on the exploit, or at least the proof-of-concept, when CC focuses on identifying a vulnerability and being able to measure its gravity and exploitability: performing a PoC is an unnecessary cost during an evaluation
 - last, but not least, CC focuses on gray-box and white-box testing, allowing for lots of shortcuts compared to a "real" (read: "black-box") pentest 

This set of documents and resources intends to help an evaluator in the course of performing a vulnerability analysis in the context of a **software CC evaluation at the level AVA_VAN.3**. This makes it somehow relevant as well for standards such as FitCEM/CSPN/BSZ, that are meant as simplified versions of this standard at this specific level.

# Disclaimer
This set of documents and resources are a work in progress, and will likely always be only that. It is mainly built as I am learning pentesting, coming from less technical parts of CC. It is updated without a formal review process, as a part of the learning process itself. 

For this reason, it should not be considered an authoritative resource: it is neither complete, nor error-free.

It should rather be used as a companion document for evaluators trying to build their own method, and should be questioned at each step!

The method also assumes that the reader has some working knowledge of the CC AVA_VAN.3 requirement, which implies the knowledge of the associated jargon: attack potential, TOE, TSF, and so on. 

# Table of contents
The main methods are based on the general type of TOE to be evalauted

 - [Linux system pentesting](_0_Linux_pentest/0_Linux_system_pentesting.md) is a method for pentesting applicative TOEs that run on Linux, or full systems based on a Linux OS
 - [Windows system pentesting](...) [not yet planned] 
 - [Mobile system pentesting](...) [not yet planned]

The evaluator should select the appropriate sections depending on the TOE type and technology:

The following supporting methods are also provided:
 - Code review methods:
     - [C code review](_0_Linux_pentest\Code_review\C_code_review_VAN3.md)
     - Python code review [planned but not started yet] 
 - [Public vulnerability analysis](_1_Public_vulnerability_analysis/Public_vulnerability_analysis_101.md)[planned but not started yet]

 


# Some context and main principles

AVA_VAN.3+ testing shares some common points with pentesting - however it also differs from it on several key points:
 - The evaluator is in a **white box** situation, and will often have a **privileged account** on the TOE to be tested. This is partly true even in a BSZ/CSPN evaluation: even if source code is not available, a privileged access to the TOE is provided.
 - Not only this, but the evaluator is in a **chosen white box**, in the sense that they can ask clarification/edits to the documentation as they see fit (within the limits of the CC requirements)
 - The analysis relies on the scoring of attacks on an attack potential scale, which means that the evaluator **does not have to actually perform attacks** whenever a vulnerability is scored as low enough.   

The main issues for the evaluator are
 - not asking enough good questions on the documentation makes you act as in a blackbox situation and lose time. You _must_ participate in the ADV review!
 - As in pentesting, if you act without a clear goal, you will probably not find anything in a constraint time frame. Apply "hack tricks" in various directions, without even being sure that they are actually relevant for the TOE security problem definition, will lead to nothing.
 - As you have many paths to assess a vulnerability, you need to use the fastest one. Some tools of the trade are also useless (e.g direct password attack is useless because you have a direct access to the passwors policy. Here you should simply give an expert opinion on the policy itself)

Therefore, the evaluator always needs to ask themselves at each step:
 - What am I trying to achieve? (i.e. what are my objectives and _attack scenarios_?) 
 - What are the resources I can use? (i.e. what are the available _attack vectors_)
 - What can I use to exploit these resources? (_method and tools_)

This method mainly aims at providing a **limited set of choices for the each question**, so that the evaluator does not get lost during their assessment. 

