# Twin Video Generation

Twins can generate **realistic talking-head videos** using their cloned voice and trained intelligence—enabling lifelike, video content. The video generation pipeline utilizes text/audio inputs and turns them into animated facial movements, producing engaging visual representations of the twin.


## Full Video Generation

In this mode, the **entire video is processed** before being made available. It ensures smoother playback and is ideal for cases where latency is not critical—such as educational content, video replies, or scripted speeches.

It's further of 2 types:

### Video generation from image link:
An input along with an image url of choice required.

### Video generation from twinId:
An input with a twinId required. The twinId takes care of the voice and image to be used, accessing them from the database.
