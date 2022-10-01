---
layout: post
title: "SDN Forensics: Why, How, and Where from here"
author: samriddha
categories: [networks, security, SDN, forensics]
image: assets/images/7764293-fig-1-source-small.gif
featured: true
---

In this write-up, I will describe what SDNs are, why forensic analysis of SDNs is a big deal, and the ways in which we do this today.

<!--more-->

## What are SDNs?

SDN stands for Software Defined Networking. It is called software-defined as the network is controlled by software-based controllers or application programming interfaces (APIs). These add a layer of abstraction over the hardware components of the networks. This paradigm centralizes the control of the network, which simplifies network administration. Also it allows the implementation of open standards, eliminating the need for vendor-specific protocols. However, it exposes several new vulnerabilities which have not yet been fully researched on.

## How is SDN Forensics any different to Traditional Network Forensics?

In regular, or Traditional, networks, threat detection and analysis is dependent on location and distribution of packets and other information. However, the centralization of control in SDNs means that evidence collection processes need an overhaul.

SDNs have three layers - Application, Control, and Infrastructure. Let us discuss the evidence collection in each of them.

![img1](/assets/images/7764293-fig-1-source-small.gif)
  
*Fig 1: An overview of the SDN architecture*

At the application layer, logs are the most useful resource. These can be retrieved in the OpenDaylight (ODL) controller by using the Open Services Gateway initiative (OSGi) architecture. These are basically additional API plugins which can be installed to retrieve information.

In the control layer, host tracking service (HTS) and link discovery service (LDS) are the two main tools. These monitor inbound and outbound traffic in the network and switches and as such can detect anomalies in the same.

At the infrastructure layer, the physical switches and the associated OpenFlow network rules can trace back malicious activity.

## What are current techniques in use in SDN Forensics?

**Packet Traceback**: Packet Traceback means determining how a packet could have arrived at a point of observation. The SDN’s packet processing behavior can be converted to a network policy. Using the policy, the back-policy can be determined using the mathematics of inverting a function. This helps us determine where a packet might have come from, given its current state and location.

**Packet Probing**: Specialized packets are used to probe the various ports and devices in the network. Using the results the entire network can be mapped.  First it is checked if the host is reachable. Then the IP and MAC addresses of the network are mapped. Once this is done, it sends probing packets of the type ARP, ICMP, TCP and UDP to the destination host and analyzes the received responses.

**SDN monitoring using PVPs**: Provenance Verification Points (PVPs) make use of the perspective that the network itself can be used as an observation point for a forensic system. These are middleboxes that collect forensic information, while allowing the network to operate normally without an excessive drop in performance.

**Forensic Management Layer**: A Forensic Management Layer (FML) is a monitoring framework designed to detect network anomalies. It is of two types - C-FML and D-FML, where ’C’ and ’D’ refer to Centralized or Distributed. C-FML monitors the traffic passing through the southbound interface. It records the requests made and responses received by the controller and the southbound interface. It is typically used when there is only one controller. D-FML monitors the east and west-bound traffic. The east and west interfaces send updates to each other thorugh the D-FML. D-FML helps guard against attacks by maintaining integrity of the network through cross-referencing the east and west interfaces.

## So let's talk about Attack Graphs

An attack graph is a succinct representation of all paths through a system that end in a state where an intruder has successfully achieved his goal. Hence, in the simplest of terms, an attack graph is a state diagram, with the end state being one which is compromised. Generating attack graphs therefore can help predict attack vectors which haven't yet been implemented by bad actors in a real attack. Hence it is an active defense measure.

We shall discuss OSSEC as a data collection tool and an algorithm to generate the attack sequence.

OSSEC is a scalable, multi-platform, open source Host-based Intrusion Detection System (HIDS). Host-based Intrusion Detection Systems run in the background. They report any abnormal activity in the system. HIDS can be configured to monitor file deletion, privilege escalation, failed authentication attempts and the like.

While OSSEC is useful for detecting and logging activities, it does not have a graphical interface. To improve the user experience, Kibana with Elasticsearch can be used. Elasticsearch is a distributed, RESTful search and analytics engine. Kibana is a free and open user interface that helps visualize the Elasticsearch data.

I haven't been able to find an algorithm specific to SDNs to generate attack graphs with raw data, however this algorithm, originally designed for traditional networks, seems to provide a headway into this problem.

![img2](/assets/images/4406402-fig-3-source-small.gif)
  
*Fig 2: An algorithm to generate Attack Graphs*

This algorithm generates the longest sequence of events where one event leads to the other, and the probabilities associated with the same. This algorithm is similar to a classic mining algorithms to find association between sets of items in a large database (which is essentially the task at hand).

## Where next?

As SDNs and allied technologies gain prominence, more and more novel attacks will be discovered. Research into SDN Forensics is greatly needed to secure our next generation of networks, specially wide area networks of essential services, given the recent rise of state-sponsored cyberattacks and increasing dependence on these networks.

## References

[1] S. Khan, A. Gani, A. W. A. Wahab, A. Abdelaziz, K. Ko, M. K. Khan, and M. Guizani, ”Software-Defined Network Forensics: Motivation, Potential Locations, Requirements, and Challenges”

[2] H. Zhang, J. Reich, and J. Rexford, ”Packet Traceback for Software-Defined Networks”

[3] S. Achleitner, T. La Porta, T. Jaeger, and P. McDaniel, ”Adversarial Network Forensics in Software Defined Networking”

[4] A. Bates et al, ”Let SDN Be Your Eyes: Secure Forensics in Data Center Networks”

[5] S. Khan et al, ”FML: A novel Forensics Management Layer for Software Defined Networks”

[6] F. Capobianco et al, ”Employing Attack Graphs for Intrusion Detection”

[7] Z. Li, J. Lei, L. Wang, and D. Li, ”A Data Mining Approach to Generating Network Attack Graph for Intrusion Prediction”

_Thanks for reading! I hope you’ve enjoyed reading this article. You can find me on_ [_Linkedin_](https://www.linkedin.com/in/samriddha-sinha/) _and_ [_GitHub_](http://github.com/sam-india-007).
