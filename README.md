# Personalized Online Learning Course: BPMN and Workflow Net Analysis

## Project Overview

This repository contains the modeling and analysis of a personalized online learning course scenario, conducted as a project for the **Business Project Modelling** course at the University of Pisa (Academic Year 2024/2025).

The goal was to model the end-to-end learning process, including administrative, scheduling, and educational phases, using **BPMN (Business Process Model and Notation)** and then translate the models into **Workflow Nets (WF-nets)** to formally verify their behavioral properties (soundness, boundedness, and liveness).

The process involves three main actors: the **Student**, the **Teacher**, and the **School's Secretariat**.

## Process Phases

The overall process is divided into the following phases:

1.  [cite_start]**Initialization Phase:** Student contacts the Secretariat, receives the course list, selects a course, gets assigned a Teacher, and makes the first installment payment. [cite: 40, 42]
2.  [cite_start]**Scheduling Phase:** Iterative exchange between the Teacher (proposing the schedule) and the Student (accepting or requesting changes) until the meeting schedule is fixed. [cite: 44, 47]
3.  [cite_start]**Lesson Execution Phase:** The core educational loop, including concept explanation, student questions, exercise attempts, and material upload by the Teacher. [cite: 48, 56]
4.  [cite_start]**Post-Lesson Interaction:** The Student reviews materials and interacts with the Teacher via chat until the materials consultation is complete. [cite: 60, 63]
5.  [cite_start]**Lesson Iteration Control:** The Teacher checks the calendar to proceed to the next lesson or transition to the Final Examination Phase. [cite: 65, 67]
6.  [cite_start]**Final Examination Phase:** Teacher assesses the student, formulates a grade, and communicates it to the Secretariat, followed by the Student's final installment and receipt of the certificate. [cite: 70, 72]

## Modeling and Analysis Tools

* [cite_start]**BPMN Modeling:** Camunda Modeler [cite: 32]
* [cite_start]**Workflow Net Analysis:** WoPeD (Workflow Petri Net Designer) [cite: 90]

## Analysis Results Summary

The process was modeled as a **BPMN Collaboration Diagram**  involving two Pools (Student and School, with two Lanes for Secretariat and Teacher). These were then translated into individual Workflow Nets for the School and the Student, and finally combined into a Workflow Module.

### Individual Workflow Net Analysis (WF-nets)

| Model | Places | Transitions | Arcs | Soundness Check | Key Properties |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **School** | 41 | 46 | 92 | **✔ Sound** | Bounded, Live, Properly Initialized. [cite_start]No free-choice violations. [cite: 122, 124, 159] |
| **Student (Base)** | 43 | 47 | 96 | **✔ Sound** | Bounded, Live, Properly Initialized. [cite_start]No free-choice violations. [cite: 127, 129, 185] |
| **Student (Variant)** | 46 | 51 | 104 | **✔ Sound** | Includes optional restart mechanism. [cite_start]Bounded, Live, Free-choice, Well-structured. [cite: 133, 135] |

### Workflow Module Analysis (Integrated Model)

The Workflow Module combines the **School WF-net** and the **Student Variant WF-net** to verify compatibility and synchronization. [cite_start]This variant was chosen as it represents the most complete process, including the optional restart mechanism. [cite: 216, 219]

* [cite_start]**Overall Result:** **✔ Sound** (Bounded and Live) [cite: 220, 221, 249]
* [cite_start]**Structural Note:** The analysis reported **6 Free-choice violations** and high numbers of PT-Handles (218) and TP-Handles (227). [cite: 222, 237, 247, 248]
* [cite_start]**Interpretation:** Despite the structural complexity indicated by the handles (shared input places reducing independence), the overall process is sound, meaning every execution can reach the final marking and no deadlocks occur. [cite: 224, 229] [cite_start]The cycles in the coverability graph reflect the correct implementation of the restart mechanism and repeated interactions. [cite: 227]

## 📂 Repository Structure (Suggested)
