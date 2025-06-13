# Twin LLM Video Generation

Twins can generate **realistic talking-head videos** using their cloned voice and trained intelligence—enabling lifelike, video content. The video generation pipeline utilizes text/audio inputs, generates repsonse via our in-house Persona LLM and turns them into animated facial movements, producing engaging visual representations of the twin.


## Full Video Generation

In this mode, the **entire video is processed** before being made available. It ensures smoother playback and is ideal for cases where latency is not critical—such as educational content, video replies, or scripted speeches.


### Video generation from twinId:
An input with a twinId required. The twinId takes care of the voice and image to be used, accessing them from the database.

## Additional parameters for the LLM case:
As opposed to the non-LLM video generation(refer to Video Generation Operations/Wihtout LLM/Video From Twin Id), wherein the twinId and input were the only required parameters, here, some new parameters are required, namely :

1. userId
2. personalityId
3. sessionId
4. wordLimit (optional, set to 50 by default, note that this number is only a rough estimate as to how many words would the response be consisting) 
5. modelName (optional, set to gpt-4 by default)
6. language  (optional, set to english by default)

## Chatting With Persona LLM:
In order to make use of our in-house Persona LLM, its necessary to create a chat(Q and A) in our backend. For such a session to be made, 3 parameters are necessary : 

A. userId: This is the unique id assigned to each user by Persona. To create your own, refer to Personality Operations/User Operations/Create New User. To use an existing userId, refer to Personality Operations/Personality Manipulation Functions/Get Persona User Id By Email.

B. personalityId: This is the unique id assigned to each personality(the digital twin in question). To create and train your own, refer to Personality Operations/Personality Manipulation Functions/Create Personality. To use an existing personality, refer to Personality Operations/Personality Manipulation Functions/Get Personality Id By Twin Id.

C. sessionId: This is the unique id assigned to each chat session(between a user and a personality). To create one, refer to Personality Operations/Chat Session Operations/Create Session.