
## Testing Phases

> ==Don’t force a name, understand the concepts.==

### Unit Testing
- Ensures that each function/bit of code works on its own and as expected
- Toolboxes like JUnit allow these to be quickly implemented and performed
- Performed by a solo developer many times per day/every new code created
- Either a pass or fail is the result

### Integration testing:
- Performed by the developer team (different functions are made by different people so it makes sense that everyone is involved) - open-box.
- Frequency of this is at the end of a sprint (e.g. 2 weeks’ work)
- Bug reports are produced if there is an issue
- Looking at multiple scripts working together rather than a single script
- Becomes more difficult to check every possible input for every possible task - missing one dependency in one class fails all other classes.
Smaller subsystems can be integrated and tested, which may then be included in another subsystem with other functions, which is then in the overall system with all its subsystems.

### Release testing
Happens after unit and subsystem integration testing; once the system is ready and can be wholly tested, **verifying it works together to meet specifications AND non-functional requirements.** 
- The last “quality check” - checking it is done and ready for the client
- Used when the software is ready to be shown to the client - it is stable enough to be revealed
- Tested typically by a ”testing team” that performs the test on the system for reliability and scalability - producing bug reports
- ”Signed off” (or not) for progression to acceptance tests
- Closed-box test on built executables

There are 3 major strategies for release testing:
Performance driven strategy:
- Testing the system’s nonfunctional requirements, e.g. scalability, performance, responsiveness, reliability, downtime, stress tests
- Reveals how many 

High-level spec-driven strategy:
- Develops a series of tests that relate to different specifications

Scenario-driven strategy:
- Uses scenarios identified during requirements gathering to roleplay as a persona to show that a standard customer scenario can be performed
- Also tries to break the scenario

### Acceptance testing
- Is the client ready to pay?
- The software is put into the hands of the client; it confirms the software that is built meets all requirements and specifications. **Only once it meets the requirements, the payment is made.**
- Iterative process and does not happen once (ideally, acceptance happens throughout the development process)
- The QA Team and Customer work together to validate and check the software
- Bugs are reported in a bug report
- **The last opportunity to discover and correct gaps before the software is released to end users.**
- May need to go the client’s side, setting up machines‘ hardware and software, using real data vs dummy data (also requires more abstract things e.g. training about how it runs, live demos, recorded sessions)
Ideally, the client has already accepted, provided additional feedback, clarified ambiguity in the requirements, low-fidelity prototype, high-fidelity design, mid-fidelity functioning prototype, and the final system.

### User testing
User/customer testing is then outside of the developer team with the own users of the x



