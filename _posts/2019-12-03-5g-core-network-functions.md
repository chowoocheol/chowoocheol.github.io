---
title: 5G Core Network Functions
layout: post
---

**Network Functions (NFs)**

* **Access and Mobility Management function (AMF) supports:** 
 Termination of NAS signalling, NAS ciphering & integrity protection, registration management, connection management, mobility management, access authentication and authorization, security context management. 
> AMF has part of the MME functionality from EPC world

* **Session Management function (SMF) supports:** 
session management (session establishment, modification, release), UE IP address allocation & management, DHCP functions, termination of NAS signalling related to session management, DL data notification, traffic steering configuration for UPF for proper traffic routing. 

* **User plane function (UPF) supports:**
packet routing & forwarding, packet inspection, QoS handling, acts as external PDU session point of interconnect to Data Network (DN), and is an anchor point for intra- & inter-RAT mobility. 
>UPF has part of the SGW & PGW functionality from EPC world

* **Policy Control Function (PCF) supports:** 
unified policy framework, providing policy rules to CP functions, access subscription information for policy decisions in UDR. 
> PCF has part of the PCRF functionality from EPC world

* **Authentication Server Function (AUSF) acts as an authentication server.** 
part of HSS from EPC world

* **Unified Data Management (UDM) supports:** 
generation of Authentication and Key Agreement (AKA) credentials, user identification handling, access authorization, subscription management. 
> part of HSS functionality from EPC world

* **Application Function (AF) supports:** 
application influence on traffic routing, accessing NEF, interaction with policy framework for policy control. 
> same as AF in EPC world

* **NF Repository function (NRF) supports:** 
service discovery function, maintains NF profile and available NF instances. 

* **Network Exposure function (NEF) supports:** 
exposure of capabilities and events, secure provision of information from external application to 3GPP network, translation of internal/external information. (not present in EPC world)
> Not present in EPC world

* **Network Slice Selection Function (NSSF) supports:** 
selecting of the Network Slice instances to serve the UE, determining the allowed NSSAI, determining the AMF set to be used to serve the UE.
> Not present in EPC world