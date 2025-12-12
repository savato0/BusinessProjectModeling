# Personalized Online Learning Course: BPMN and Workflow Net Analysis

## Project Overview

This repository contains the modeling and analysis of a personalized online learning course scenario, developed as a project for the **Business Project Modelling** course at the **University of Pisa** (Academic Year 2024/2025).

The project focuses on modeling the end-to-end learning process—including administrative, scheduling, and educational phases—using **BPMN (Business Process Model and Notation)**. The models were subsequently translated into **Workflow Nets (WF-nets)** to formally verify their behavioral properties, such as soundness, boundedness, and liveness.

## Scenario & Actors

The process involves three main actors:
1.  **Student:** The primary initiator who selects courses, pays installments, and interacts with the teacher.
2.  **Teacher:** Responsible for scheduling, delivering lessons, assigning exercises, and evaluating the student.
3.  **School's Secretariat:** Manages the initial course list, teacher assignment, and final certification.

### Process Phases
The workflow is divided into the following logical phases:
* **Initialization:** Course selection, teacher assignment, and first payment.
* **Scheduling:** Negotiation of the lesson calendar between Student and Teacher.
* **Lesson Execution:** The core loop of teaching, Q&A, and exercise assignment.
* **Post-Lesson Interaction:** Asynchronous chat and material study.
* **Iteration Control:** Decision point to continue lessons or proceed to the exam.
* **Final Examination:** Assessment, grading, final payment, and certification.

## Tools Used

* **Modeling:** [Camunda Modeler](https://camunda.com/) (for BPMN Collaboration Diagrams)
* **Analysis:** [WoPeD](https://woped.dhbw-karlsruhe.de/) (Workflow Petri Net Designer for WF-net analysis)

## Analysis Results

The project involved creating a BPMN collaboration diagram and converting it into Workflow Nets. Below are the quantitative and qualitative analysis results for each component.

### 1. Individual Workflow Nets
The BPMN pools were converted into separate WF-nets for the School (Teacher + Secretariat) and the Student.

| Model | Places | Transitions | Arcs | Soundness | Properties |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **School** | 41 | 46 | 92 | **✅ Sound** | Bounded, Live, Well-structured. |
| **Student (Base)** | 43 | 47 | 96 | **✅ Sound** | Bounded, Live, Well-structured. |
| **Student (Variant)** | 46 | 51 | 104 | **✅ Sound** | Includes optional restart mechanism. Bounded, Live. |

### 2. Workflow Module (Integrated Analysis)
The **Student Variant** and **School** nets were combined into a single **Workflow Module** to verify the compatibility of the message exchanges and the overall process synchronization.

* **Overall Result:** **✅ Sound**
* **Boundedness:** The net is bounded (no infinite token accumulation).
* **Liveness:** The net is live (no dead transitions).
* **Structural Notes:** The complex interaction resulted in 6 free-choice violations and several PT/TP handles, indicating shared resources/paths. However, the semantic analysis confirmed that these did not negatively impact the logical correctness or reachability of the final state.

## Conclusion
The modeling and analysis confirm that the proposed process for the personalized online learning course is robust. Both the individual processes and their composition are sound, bounded, and live, ensuring that every student who begins the course can successfully complete it (or restart it) without encountering deadlocks or synchronization errors.
