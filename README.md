# 🎤 LiveKit Intelligent Interruption Handler

This project implements an intelligent interruption mechanism for real-time voice agents.  
The system separates **backchannel acknowledgements** (e.g., "yeah", "ok", "hmm") from **true interruptions** (e.g., "stop", "wait", "no"), ensuring smooth conversational flow without accidental speech cutoffs.

---

## 🔥 Key Objective

Fix the default LiveKit behavior where the agent wrongly stops speaking when the user says short filler words.

### Required Behavior

| User Input | Agent Speaking? | Expected Action |
|-----------|----------------|----------------|
| yeah / ok / hmm | ✔ Yes | **IGNORE — continue speaking** |
| stop / wait / no | ✔ Yes | **INTERRUPT — stop immediately** |
| yeah / ok | ✘ No | **RESPOND normally** |
| "yeah wait" | ✔ Yes | **INTERRUPT (mixed command detected)** |

---

## 🧠 How It Works

The **IntelligentInterruptionHandler** performs:

1. Detects whether the AI agent is currently speaking  
2. Categorizes the user input into:
   - **ignore_words** → backchannel acknowledgement
   - **interrupt_words** → intent to stop agent
3. Applies real-time decisions with minimal delay
4. Supports multi-word checking + mixed sentence detection

```python
self.ignore_words = ["yeah", "ok", "hmm", "right", "uh-huh"]
self.interrupt_words = ["stop", "wait", "no"]
