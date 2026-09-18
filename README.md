# 🌾 Kisan Voice Advisor (کسان وائس ایڈوائزر)

**Kisan Voice Advisor** is an AI-powered agricultural assistant designed specifically for Pakistani farmers. It breaks literacy and technological barriers by allowing farmers to ask questions via Urdu speech, upload leaf photos for computer-vision disease detection, and receive natural Urdu spoken advice. It also includes an interactive **Farm Simulator** game to help farmers practice resource management and decision-making.

---

## 🌟 Key Features

### 1. 🎙️ Urdu Voice Advisor
- **Speech-to-Text (STT):** Transcribes recorded Urdu audio using Groq’s high-performance `whisper-large-v3-turbo` model.
- **Orchestration Backend:** Routes agricultural queries to an `n8n` workflow webhook connected to domain-specific knowledge bases.
- **Neural Text-to-Speech (TTS):** Converts Urdu responses back into realistic, natural spoken audio using `edge-tts` (`ur-PK-AsadNeural`).

---

### 2. 📷 Crop Disease Identification
- **Computer Vision Model:** Leverages a pre-trained `MobileNetV2` model fine-tuned on plant disease datasets (`linkanjarad/mobilenet_v2_1.0_224-plant-disease-identification`).
- **Automated Treatment Plans:** Extracts predicted disease labels, queries the backend agent, and presents an Urdu treatment plan with voice output.
- **Confidence Validation:** Displays confidence scores and screens out low-confidence/non-leaf images.

---

### 3. 🎮 Interactive Farm Simulator
- **Multi-Round Strategy:** Simulates a 6-round crop growth cycle (Wheat, Cotton, or Rice) from sowing to harvest.
- **Resource Management:** Tracks yield projections, water levels, and financial capital based on user choices.
- **In-Game AI Assistance:** Allows players to consult the AI advisor directly mid-game before committing to critical farming decisions.

---

### 4. 🎨 Customized Streamlit Interface
- Custom dark-green agriculture-themed UI built with embedded CSS animations and floating background graphics.
- JavaScript injection to style sandboxed iFrames (e.g., `streamlit_mic_recorder`).
- Animated splash loader screen upon application startup.

---

## 🏗️ System Architecture

```text
  [ User Speech / Leaf Photo ]
               │
               ▼
   [ Streamlit Frontend UI ]
      │               │
      ├── (Audio) ───► [ Groq Whisper API ] ──────┐
      │                                           │ (Urdu Text)
      └── (Photo) ───► [ Local MobileNetV2 ] ────┤
                                                  ▼
                                       [ n8n Webhook Backend ]
                                                  │
                                                  ▼ (Urdu Response)
   [ Spoken Urdu Audio ] ◄── [ Edge TTS ] ◄───────┘
