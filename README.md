# real-time-voice-transcriptionn-by-me
 import libraries. Streamlit is used for building the app interface, and speech_recognition is used for audio processing and transcription.  We define a function transcribe_audio() that handles the audio transc Inside this func We create a speech recognizer object using sr.Recognizer(). We use the default microphone as the audio source





# code ######
import streamlit as st
import speech_recognition as sr

def transcribe_audio():
    # Create a recognizer object
    r = sr.Recognizer()
    
    # Use the default microphone as the audio source
    with sr.Microphone() as source:
        # Adjust for ambient noise
        r.adjust_for_ambient_noise(source)
        
        # Prompt the user to speak
        st.write("Speak something...")
        
        # Record the audio
        audio = r.listen(source)
        
        # Use the SpeechRecognition library to transcribe the audio
        try:
            # Perform speech recognition
            text = r.recognize_google(audio)
            return text
        except sr.UnknownValueError:
            return "Could not understand audio"
        except sr.RequestError as e:
            return f"Error: {e}"
            
def main():
    st.title("Real-time Voice Transcription App")
    
    # Start the transcription process when the user clicks the button
    if st.button("Start Transcription"):
        transcribed_text = transcribe_audio()
        st.write("Transcribed Text:")
        st.write(transcribed_text)
        
if __name__ == '__main__':
    main()
