# An Electronic Examination Model Based on UPPAAL

Electronic examinations offer a convenient way for assessing the knowledge and abilities of learners with the help of computer and network technologies. In this study, we employ UPPAAL to formally model and analyze the electronic examination process, including conduction of four templates and verification of twelve properties. 

## Table of Contents

- [Background](#Background)
  - [Roles of Participants](#Roles-of-Participants)
  - [Simulation and Verification](#Simulation-and-Verification)
- [Model Specifications](#Model-Specifications)
  - [Candidate Template](#Candidate-Template)
  - [Administrator Template](#Administrator-Template)
  - [Invigilator Template](#Invigilator-Template)
  - [Examiner Template](#Examiner-Template)
- [Property Specifications](#Property-Specifications)
  - [No Deadlock](#No-Deadlock)
  - [Candidate Registration](#Candidate-Registration)
  - [Candidate Eligibility](#Candidate-Eligibility)
  - [Answer Authentication](#Answer-Authentication)
  - [Answer Singularity](#Answer-Singularity)
  - [Acceptance Assurance](#Acceptance-Assurance)
  - [Question Ordering](#Question-Ordering)
  - [Exam Availability](#Exam-Availability)
  - [Answer-Score Integrity](#Answer-Score-Integrity)
  - [Cheater Detection](#Cheater-Detection)
  - [Marking Correctness](#Marking-Correctness)
  - [Mark Integrity](#Mark-Integrity)  
- [Verification Results](#Verification-Results)


## Background

### Roles of Participants

In a general way, there are four roles in an electronic examination, i.e., candidate, administrator, invigilator and examiner. We list their functions as follows. 
* Candidate: A candidate is a student taking the examination.
* Administrator: An administrator is responsible for registering candidates for the examination.
* Invigilator: An invigilator is tasked with distributing questions, supervising the examination and collects answers. 
* Examiner: A examiner marks the examination and notifies students their scores. 
Each participant is assigned specific tasks, and through collaborative efforts, they contribute to the successful execution of electronic examinations.

### Simulation and Verification

When simulating this model (i.e., [An-Electronic-Examination-Model-Based-on-UPPAAL.xml](https://github.com/TURTING-BO/An-Electronic-Examination-Model-Based-on-UPPAAL/blob/main/An-Electronic-Examination-Model-Based-on-UPPAAL.xml), ensure that you have installed UPPAAL Tools. You can download CPNs Tools from the website "https://uppaal.org/". The site provides numerous helpful tutorials on effectively utilizing this powerful tool.

## Model Specifications

In our model, there are four templates corresponding to the candidate, administrator, invigilator, and examiner, as follows.

### Candidate Template

<figure>
  <div align=center>
    <img src="https://github.com/TURTING-BO/An-Electronic-Examination-Model-Based-on-UPPAAL/blob/main/Template%20Figures/Candidate%20Template.jpg" width="70%" height="70%">  
  </div>
  <div align=center>
     <figcaption>Figure 1. Candidate Templates</figcaption>
  </div>    
</figure>

### Administrator Template
<figure>
  <div align=center>
    <img src="https://github.com/TURTING-BO/An-Electronic-Examination-Model-Based-on-UPPAAL/blob/main/Template%20Figures/Administrator%20Template.jpg" width="70%" height="70%"> 
  </div>
  <div align=center>
     <figcaption>Figure 2. Administrator Templates</figcaption>
  </div>    
</figure>

### Invigilator Template
<figure>
  <div align=center>
    <img src="https://github.com/TURTING-BO/An-Electronic-Examination-Model-Based-on-UPPAAL/blob/main/Template%20Figures/Invigilator%20Template.jpg" width="70%" height="70%"> 
  </div>
  <div align=center>
     <figcaption>Figure 3. Invigilator Templates</figcaption>
  </div>    
</figure>

### Examiner Template
<figure>
  <div align=center>
    <img src="https://github.com/TURTING-BO/An-Electronic-Examination-Model-Based-on-UPPAAL/blob/main/Template%20Figures/Examiner%20Template.jpg" width="70%" height="70%"> 
  </div>
  <div align=center>
     <figcaption>Figure 4. Examiner Templates</figcaption>
  </div>    
</figure>

## Property Specifications

### No Deadlock

In the electronic examination model, the absence of deadlocks is crucial to prevent any "never-ending" scenarios.

<p align="center" > A[] not deadlock </p>

### Candidate Registration

The candidate registration property stipulates that a candidate can submit an answer only if they have registered.

<p align="center"> A[] forall(i:ID) !(! FindElement(R, i) & FindElement(S, i)) </p>

### Candidate Eligibility

The candidate eligibility property signifies that a candidate's answer can be accepted only if they have registered.

<p align="center"> A[] forall(i:ID) !(!FindElement(R, i) & FindElement(A, i)) </p>

### Answer Authentication

The answer authentication property stipulates that a candidate's answer can be accepted only if they have submitted the answer.

<p align="center"> A[] forall(i:ID) !(!FindElement(S, i) & FindElement(A, i)) </p>

### Answer Singularity

The answer singularity property signifies that, for each candidate, only a singular response can be deemed acceptable per question.

<p align="center"> A[] forall(i:ID) OneAnswerEachQuestion(A, i) </p>

### Acceptance Assurance

The acceptance assurance property underscores the requirement that an answer submitted by a candidate should be accepted.

<p align="center"> A[] forall(i:ID) FirstSubmitFollowAccept(T, i) </p>

### Question Ordering

The question ordering property emphasizes that a candidate can proceed to the next question only after the answer to the current question is accepted.

<p align="center"> A[] forall(i:ID) GetAcceptGet(T, i) </p>

### Exam Availability

The exam availability property stipulates that the acceptance of an answer from a candidate is permissible only during the examination period.

<p align="center"> A[] StartAcceptEnd(T) </p>

### Answer-Score Integrity

The answer-score integrity property ensures that the correct answer can not be modified after the examination starts.

<p align="center"> A[] NoStartCorrAns(T) </p>

### Cheater Detection

During an examination process, cheating may take place, e.g., one candidate copies the answers of the other candidate.

<p align="center"> A[] NoDistanceExceed(sm) </p>

### Marking Correctness

The marking correctness property asserts that once marking has occurred, the correct answers cannot be modified. 

<p align="center"> A[] NoCorrAnsMark(T) </p>

### Mark Integrity

The mark integrity property ensures that each candidate receives notification after marking, and all answers from candidates are duly marked.

<p align="center"> A[] MarkIntegrity(T) </p>

## Verification Results
Our model satisfied all the 12 specified properties, underscoring the reliability of the electronic examination model. The verification time and resident memory statistics indicate that the associated time and space overhead are within acceptable limits.

<figure>
  <div align=center>
    <img src="https://github.com/TURTING-BO/An-Electronic-Examination-Model-Based-on-UPPAAL/blob/main/Verification%20Results.jpg" width="70%" height="70%"> 
  </div>
  <div align=center>
     <figcaption>Figure 5. Verification Resultss</figcaption>
  </div>    
</figure>
