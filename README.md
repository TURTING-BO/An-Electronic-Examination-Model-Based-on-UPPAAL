Formal Modeling and Verification of Electronic Examination Based on UPPAAL

Electronic examinations offer a convenient way for assessing the knowledge and abilities of learners with the help of computer and network technologies. The participants in electronic examinations are akin to those in traditional exams, with the difference that certain operations are conducted through network communications.

#1 Roles of Participants
In a general way, there are four roles in an electronic examination, i.e., candidate, administrator, invigilator and examiner. We list their functions as follows. 
>> Candidate: A candidate is a student taking the examination.
>> Administrator: An administrator is responsible for registering candidates for the examination.
>> Invigilator: An invigilator is tasked with distributing questions, supervising the examination and collects answers. 
>> Examiner: A examiner marks the examination and notifies students their scores. 
Each participant is assigned specific tasks, and through collaborative efforts, they contribute to the successful execution of electronic examinations.

#2 Model Specification
In our model, there are four templates corresponding to the candidate, administrator, invigilator, and examiner, as follows.
>> Candidate Template
>> Administrator Template
>> Invigilator Template
>> Examiner Template

#3 Property Specifications
(1)	No Deadlock
In the electronic examination model, the absence of deadlocks is crucial to prevent any "never-ending" scenarios.
A[] not deadlock
(2)	Candidate Registration
The candidate registration property stipulates that a candidate can submit an answer only if they have registered.
A[] forall(i:ID) !(! FindElement(R, i) & FindElement(S, i))
(3)	Candidate Eligibility
The candidate eligibility property signifies that a candidate's answer can be accepted only if they have registered.
A[] forall(i:ID) !(!FindElement(R, i) & FindElement(A, i))
(4)	Answer Authentication
The answer authentication property stipulates that a candidate's answer can be accepted only if they have submitted the answer.
A[] forall(i:ID) !(!FindElement(S, i) & FindElement(A, i))
(5)	Answer Singularity
The answer singularity property signifies that, for each candidate, only a singular response can be deemed acceptable per question.
A[] forall(i:ID) OneAnswerEachQuestion(A, i)
(6)	Acceptance Assurance
The acceptance assurance property underscores the requirement that an answer submitted by a candidate should be accepted.
A[] forall(i:ID) FirstSubmitFollowAccept(T, i)
(7)	Question Ordering
The question ordering property emphasizes that a candidate can proceed to the next question only after the answer to the current question is accepted.
A[] forall(i:ID) GetAcceptGet(T, i)
(8)	Exam Availability
The exam availability property stipulates that the acceptance of an answer from a candidate is permissible only during the examination period.
A[] StartAcceptEnd(T)
(9)	Answer-Score Integrity
The answer-score integrity property ensures that the correct answer can not be modified after the examination starts.
A[] NoStartCorrAns(T)
(10)	Cheater Detection
During an examination process, cheating may take place, e.g., one candidate copies the answers of the other candidate.
A[] NoDistanceExceed(sm)
(11)		Marking Correctness
The marking correctness property asserts that once marking has occurred, the correct answers cannot be modified. 
A[] NoCorrAnsMark(T)
(12)	Mark Integrity
The mark integrity property ensures that each candidate receives notification after marking, and all answers from candidates are duly marked. 

#4 Verification Results
Our model satisfied all the 12 specified properties, underscoring the reliability of the electronic examination model. The verification time and resident memory statistics indicate that the associated time and space overhead are within acceptable limits.
