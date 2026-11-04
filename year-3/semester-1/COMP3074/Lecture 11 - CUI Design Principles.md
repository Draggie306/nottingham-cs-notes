

This is based on a 2017 book by Cathy Pearl: Desining Voice User Interfaces.


## Part 1. Conversational design


Voice user interfaceshave a wake word that explicity invokes the interaction, such as *Alexa, ...* or *Hey Google...* and listens for a predetermined period, e.g. until it "hears" the last input and then waits for about 2 seconds before transcribing.

The trouble with this intersectional setup is that it is not conversational: it is not how people talk. Conversational means a conversational prompt design: how the developer design the system response - what the system is saying back to the user, e.g. acknowledging a "Thank you" by saying "You're welcome". This is called a **conversational marker**. Good prompt design make use of conversational markers amongst other things.

![](../../../Images/Pasted%20image%2020261103100654.png)

Some may say this is concerning being too "human-like". These markers also serve as a utility - letting the user know where they are in conversation, within the persona of the chatbot.

Some designs keep track of **context**. What context means is a hard problem. Some solutions include:
- coreference resolution
	- different words point to the same thing
	- pronouns and indexicals: substituting "he" to be a value previously referred to.

- The user should decide how long the conversation to be, and when to initiate the conversation: the bot starting is seen to be "creepy".
- Responses should be personalised, addressing the user by name, using the location or timezone if known.
- Provide clear and actionable prompts: "Would you like to send it or change it?"
- Be concise: **speech is ephemeral** so users may not want to read huge pages of text.
- Help the user understand what they can do: discoverability is important.
- Help the user recover from errors: provide status updates about the system, but also provide contextual help.

## 2. CUI Design Process

CUIs are best created following a UX design process. There is an approach called user- or human-centred design: an ISO standard 9241. There are different design tools available: writing sample dialogues from paper, visual mockups, flow (dialogue flow design), etc.

A sample dialog avoids writing prompts in isolation which can lead to a stilted user experience. Commonly this is done by picking 5 most common use cases for the CUI, starting with the "blue sky" best path dialogs, also writing for when things go wrong.  Doing this manually is better than getting LLMs to design this.

![](../../../Images/Pasted%20image%2020261103102459.png)

https://wit.ai

## 3. Confirmations

A key part of CUI design is getting the user to confirm an action. Over-confirmation can be a problem, but there should be considerations for choosing a confirmation strategy. Consider the consrquences for getting things wrong - such as the wrong flight being booked or just the wrong location being queried for the weather forecast. 

Explicit confirmation: I think you want to do X. Is that correct?
- requires the user to take another turn

Implicit confirmation: "Okay, setting reminder to do X."
- Does not require the user to say anything else but still builds in some of the request context to ensure the user can be confident in the answer. "the weather tomorrow is X" vs "the weather in Nottingham tomorrow is X"

There are multiple confirmation methods.
- When doing intent matching, this also produces a confidence level.  The **three-tiered confidence** uses the system confidence that the user request has been interpreted correctly. For example, above 80% confidence results in an implicit conversation; between 45-79% it asks for explicit confirmation, and anything below is asked to try again. 
- **Nonspeech confirmation**: there is no response required, the action is just carried out. For example, turning on lights. 
- **Generic confirmation**. Something that works most of the time, particularly if the chatbot cannot be 100% sure on what the user said. Such as, "I'm sorry to hear that. Tell me more?"
- Visual confirmation: good for hybrid experiences. Screens are great at communicating several items of information

## 4. Error handling

When speaking to a human, there is no unrecoverable error state. **Reprompting** is the traditional way if the user was not heard or understood, "Sorry, I didn't understand". Reprompts are not always necessary - they can be rather annoying. Silence can work in the same way: silence is a sign of trouble, but does not tell the user what the problem is. 

![](../../../Images/Pasted%20image%2020261103104152.png)

If no speech is detected, this is **pre-ASR** and should be handled by an indicator, such as Alexa's light ring illuminating. 

If speech is detected but nothing recognised, calling this out explicitly ("I'm sorry, I didn't understand") is ideal - but ambiguous, as it does not tell the user if there was an error during transcription or semantic. 


Homonym resolution:
![](../../../Images/Pasted%20image%2020261103104831.png)


Progessive reprompting tells the user what is expected instead of generic error messages, an "escalating error strategy":
![](../../../Images/Pasted%20image%2020261103104909.png)


Users should not be blamed at any time for errors, and this should be designed for both novice and expert users.

### Universals

There should be a range of global commands that the user can always say. Things such as "help", "stop". Helping 