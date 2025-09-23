# 30-Day-MyDFIR-Microsoft-Challenge

## Introduction
This is a mini project based on 30-Day MyDFIR Microsoft SOC Analyst Challenge. The course is divided into four sections. It includes small assignments and 4 mini-projects that cover the following:

- section 1: SOC lab and Microsoft Sentinel setup
- section 2: Email security with Defender for Office 365
- section 3: Endpoint security with Defender for Endpoint
- section 4: Identity with Entra ID

## Goal
The goal of this challenge was to create:
- Simulated SOC environment (Microsoft SOC Lab)

## Tools 
- Microsoft Sentinel 
- Microsoft Defender for Endpoint
- Microsoft Defender for Office 365
- Entra ID

## Requirements
- A host PC
- 1 test Windows 11 virtual machine (mine was hosted in Azure)
- 1 Microsoft 365 E5 Trial (could be free, or you might have to buy)


## Table of contents

### Section 1: SOC lab setup
This section covers SOC lab and Microsoft Sentinel setup.

#### Day 0–1
- Requirements
- Resources' names
- Create a billing alert on Azure

#### Day 2
- Create a Resource Group 
- Create a Windows 11 VM in Azure
- Create an inbound rule (NSG) to restrict RDP

#### Day 3
- Deploy Microsoft Sentinel
    - Create Log Analytics Workspace in Sentinel
    - Install Microsoft Sentinel
    - Connect Sentinel to Defender XDR

#### Day 4
- Enable Azure Activity logs
- Connect Azure Activity to Sentinel
- Setup Microsoft Sentinel Training Lab
- Example KQLs

#### Day 5
- How to create a workbook
- Example KQLs with visualizations

#### Day 6
- Difference between Defender XDR and Microsoft Sentinel
- Install Microsoft Defender XDR connector
- Create Analytics rule in Defender XDR

#### Day 7-9 - Mini Project 1
- BruteForce Simulation
    - Simulation 1 — Local web client BruteForce
    - Simulation 2 — RDP-based BruteForce
- Analytics rule creation and detection
- Create a Bookmark 
 - Create an incident from a Bookmark
- Report 

#### Section 2: Email security
This section covers email security with Microsoft Defender for Office 365 and phishing investigations. 

#### Day 10
- Create new users
- Activate user's outlook mailbox
- Overview of Email & collaboration in Microsoft Defender XDR (in progress)

#### Day 11-13
Covers Policies & rules
- Safe Links Policies
- Anti-Phishing Policies
- Configuration analyzer

#### Day 14
- Reporting Phishing Email 

#### Day 15
- Simulate a Phishing attack - Method 1
- Simulate a Phishing attack - Method 2

#### Day 16 - Mini Project 2
- Simulate a phishing attack
- Write investigation report

#### Section 3: Endpoint security
This section focuses on Microsoft Defender for Endpoint and teaches endpoint investigation and threat hunting. 

#### Day 17
- What is Microsoft Defender for Endpoint
- Onboard Test VM
    - How to RDP into an Azure VM
- Install onboarding package on Test VM

#### Day 19
- What is Microsoft Intune?
- Attack Surface Reduction (ASR) Rules
- Enroll an Endpoint into Intune
    - RDP to your test VM using your test user account
- Configure ASR rules in Intune

#### Day 20
- Install Atomic Read Team
- Run Atomic Test

#### Day 21
- What is Threat Hunting
- Types of hunts
    - Structured hunting
    - Unstructured hunting
    - Situational hunting
- How to form a hypothesis
- Exercise: Hunting examples 

#### Day 22
- Simulate and hunt an activity

#### Day 23 - Mini Project 3
- Simulation of T1197 - BITS Jobs

#### Section 3: Entra ID

#### Day 24 
- Entra Admin portal
- Overview of Microsoft Entra portal
    - Entra ID
    - Conditional access
- Monitoring & health
- ID Protection

#### Day 25
- Enable the Entra ID data connector in Microsoft Sentinel

#### Day 27–29 - Mini-Project-Final – Saliha Tabbassum
- Step 1: Phishing email simulation
- Step 2: Risky sign-in and impossible travel simulation
- Step 3: Endpoint activity simulation
- Step 4: Investigation report
