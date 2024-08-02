## text to specch
```python
!pip install TTS gradio --upgrade
from TTS.api import TTS
import gradio as gr

# Initialize TTS model
tts = TTS("tts_models/multilingual/multi-dataset/xtts_v2", gpu=True)

def generate_speech(text, speaker_wav_path):
    # Generate speech and save to a temporary file
    temp_file_path = "temp_output.wav"
    tts.tts_to_file(
        text=text,
        file_path=temp_file_path,
        speaker_wav=speaker_wav_path,
        language="en"
    )
    return temp_file_path  # Return the path to the generated audio

# Create Gradio interface
demo = gr.Interface(
    fn=generate_speech,
    inputs=[
        gr.Textbox(label="Input Text"),
        gr.Audio(type="filepath", label="Speaker Audio (Optional)") # Remove the source argument
    ],
    outputs=gr.Audio(label="Generated Speech"),
    title="XTTS v2 Text-to-Speech with Voice Cloning",
    description="Enter text and optionally upload speaker audio for voice cloning."
)

# Launch the interface
demo.launch()
```
