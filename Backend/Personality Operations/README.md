# Personality Oriented Operations

This guide is about operations realted to **personalities**.

## 🧠 What is a Personality?

A **Personality** is the unison of all twin related fields like voiceID, avatar image etc. and its training data, text files as well.


## 🛠️ How It Works

Below is the overall flow for chatting with a personality:

### 1. `Create New User`

Creates a new user and returns a unique **user id**. (refer to **User Operations/Create New User**)

### 2. `Create Personality`

A new personality is created, training files, social url, name etc. are used in the process. A unique **personality id** is returned. (refer to **Personality Manipulation/Create Personality**)

### 3. `Create Session`
A new chat session is created for the text chat to commence. A **session id** is returned. (refer to **Chat Sessions Operations/Create Session**)

### 4. `Create Chat`
The text chat finally commences. Session ID and text message are taken in as input, and **response from the personality** is returned. (refer to **Text Chat Operations/Create Chat**)