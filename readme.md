# Voice Assistant with Multi-Language Support 🎤🤖

A real-time voice assistant powered by AI agents that supports multiple languages and function calling. Features live audio streaming, Spanish language handoff, and weather functionality.

## 🌟 Features

- **Real-time Voice Processing** - Live audio input and output streaming
- **Multi-Language Support** - Automatic handoff to Spanish-speaking agent
- **Function Calling** - Built-in weather tool with extensible architecture
- **Agent Handoffs** - Seamless transitions between specialized agents
- **Live Audio Streaming** - Real-time audio playback using sounddevice
- **Modular Architecture** - Easy to extend with new agents and tools

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- Microphone and speakers/headphones
- OpenAI API key (for GPT-4o-mini)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/voice-assistant.git
cd voice-assistant
```

2. Install dependencies:
```bash
pip install agents sounddevice numpy asyncio
```

3. Set up your OpenAI API key:
```bash
export OPENAI_API_KEY="your-api-key-here"
```

### Usage

Run the voice assistant:

```bash
python voice_assistant.py
```

The assistant will:
1. Start listening for voice input
2. Process your speech in real-time
3. Respond with synthesized voice
4. Automatically switch to Spanish agent if you speak Spanish

## 🏗️ Architecture

### Agent System

The application uses a multi-agent architecture with specialized roles:

```
Main Assistant Agent
├── Function Tools (Weather)
└── Handoff → Spanish Agent
```

#### Main Assistant Agent
- **Role**: Primary interaction handler
- **Model**: GPT-4o-mini
- **Capabilities**: 
  - General conversation
  - Weather queries
  - Language detection and handoff
- **Instructions**: Polite, concise responses with Spanish detection

#### Spanish Agent
- **Role**: Spanish language specialist
- **Model**: GPT-4o-mini
- **Capabilities**: Native Spanish conversation
- **Instructions**: Respond entirely in Spanish

### Voice Pipeline

```
Audio Input → Voice Recognition → Agent Processing → Text-to-Speech → Audio Output
```

## 🛠️ Technical Components

### Audio Handling
- **Input Buffer**: 3-second rolling buffer (24kHz, 16-bit)
- **Real-time Processing**: Async audio streaming
- **Output**: Live audio playback via sounddevice

### Function Tools

#### Weather Tool
```python
@function_tool
def get_weather(city: str) -> str:
    """Get the weather for a given city."""
    # Returns randomized weather for demo purposes
```

### Agent Configuration
- **Model**: GPT-4o-mini for fast response times
- **Handoff System**: Automatic language detection and routing
- **Extensible**: Easy to add new agents and tools

## 📝 Code Structure

```
voice_assistant.py
├── Imports and Dependencies
├── Function Tools Definition
├── Agent Configuration
│   ├── Spanish Agent
│   └── Main Assistant Agent
├── Audio Pipeline Setup
└── Main Execution Loop
```

### Key Components

1. **Function Tools**: Extensible tool system for agent capabilities
2. **Agent Definitions**: Specialized agents with handoff capabilities
3. **Voice Pipeline**: Real-time audio processing workflow
4. **Audio Streaming**: Live input/output audio handling

## 🔧 Configuration

### Audio Settings
- **Sample Rate**: 24kHz
- **Channels**: Mono (1 channel)
- **Bit Depth**: 16-bit
- **Buffer Size**: 3 seconds (72,000 samples)

### Agent Models
- **Primary Agent**: GPT-4o-mini
- **Spanish Agent**: GPT-4o-mini
- **Response Style**: Polite and concise

## 🌐 Multi-Language Support

### Language Detection
The main agent automatically detects Spanish input and hands off to the Spanish agent.

### Adding New Languages
To add support for additional languages:

1. Create a new agent:
```python
french_agent = Agent(
    name="French",
    handoff_description="A french speaking agent.",
    instructions=prompt_with_handoff_instructions(
        "You're speaking to a human, so be polite and concise. Speak in French.",
    ),
    model="gpt-4o-mini",
)
```

2. Add to main agent handoffs:
```python
agent = Agent(
    # ... existing config
    handoffs=[spanish_agent, french_agent],
)
```

3. Update detection instructions:
```python
instructions=prompt_with_handoff_instructions(
    "If the user speaks in Spanish, handoff to spanish agent. If French, handoff to french agent.",
)
```

## 🔨 Extending Functionality

### Adding New Tools

Create new function tools for additional capabilities:

```python
@function_tool
def get_time(timezone: str = "UTC") -> str:
    """Get the current time in a specific timezone."""
    # Implementation here
    return f"Current time in {timezone}: ..."

# Add to agent tools
agent = Agent(
    # ... existing config
    tools=[get_weather, get_time],
)
```

### Custom Agent Behaviors

Modify agent instructions for different personalities or capabilities:

```python
creative_agent = Agent(
    name="Creative",
    instructions=prompt_with_handoff_instructions(
        "You are a creative writing assistant. Help users with stories, poems, and creative content.",
    ),
    model="gpt-4o-mini",
)
```

## 🎵 Audio Requirements

### Input Device
- Any microphone (built-in or external)
- Recommended: USB microphone for better quality
- Ensure proper audio permissions

### Output Device
- Speakers or headphones
- Avoid feedback loops (use headphones when possible)

## 🐛 Troubleshooting

### Common Issues

1. **Audio Device Not Found**
   ```bash
   # List available audio devices
   python -c "import sounddevice as sd; print(sd.query_devices())"
   ```

2. **API Key Error**
   ```bash
   # Verify API key is set
   echo $OPENAI_API_KEY
   ```

3. **Module Import Error**
   ```bash
   # Install missing dependencies
   pip install --upgrade agents sounddevice numpy
   ```

### Audio Issues
- Check microphone permissions
- Verify audio device connectivity
- Test with different sample rates if needed

## 📋 Dependencies

### Core Libraries
- `agents` - AI agent framework
- `sounddevice` - Real-time audio I/O
- `numpy` - Numerical operations for audio
- `asyncio` - Asynchronous programming

### System Requirements
- Python 3.8+
- Audio input/output devices
- Internet connection for API calls

## 🔐 Security & Privacy

- Audio processing happens in real-time
- No audio data is permanently stored
- API calls follow OpenAI's usage policies
- Voice data is processed ephemerally

## 🚧 Development

### Running in Development Mode

Enable tracing for debugging:
```python
# Remove this line to enable tracing
set_tracing_disabled(True)
```

### Testing
1. Test with different languages
2. Verify tool calling functionality
3. Check audio quality and latency

## 🔮 Roadmap

- [ ] Additional language support (French, German, etc.)
- [ ] Custom wake word detection
- [ ] Voice activity detection improvements
- [ ] Integration with more external APIs
- [ ] Conversation memory and context
- [ ] Voice cloning capabilities
- [ ] Real-time translation
- [ ] Sentiment analysis
- [ ] Background noise reduction

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Add your improvements
4. Test with voice input/output
5. Submit a pull request

## 🆘 Support

If you encounter issues:

1. Check audio device permissions
2. Verify API key configuration
3. Test internet connectivity
4. Review console output for errors
5. Open an issue with system details

---

**Start talking!** 🎤✨

*Built with ❤️ using AI agents and real-time voice processing*
