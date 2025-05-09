# Surfer Mood

Final project for the Building AI course

## Summary

**SurferMood** is an AI-powered assistant that generates custom Spotify playlists adapted to your surf session, based on wave conditions, your physical data, and detected mood. -> Building AI course project.

## Background

Music is rarely personalized to match the intensity or feeling of a surf session. Many surfers enjoy listening to music before or after sessions to get in the zone or unwind. However, there's no system that connects *how you surf* with *what you hear*.

Problems this idea addresses:
- Lack of personalized music experiences for surfers
- Disconnection between mood, physical effort and playlist choice
- Missed opportunities to boost motivation or relaxation through sound

My motivation: I’m a surfer and a music lover. I want to merge these worlds to enhance the way we ride and recover.

## How is it used?

**SurferMood** is used before, during (optionally), or after a surf session. The user connects their smartwatch (for heart rate, session duration, GPS) and/or lets the app access surf spot data (via surf forecast APIs).

The app performs:
1. Analysis of surf session (speed, intensity, wave quality)
2. Mood inference (calm / excited / tired / pumped)
3. Playlist generation using Spotify API, matching mood and tempo

**Users**: Surfers with smartwatches or apps like Surfline. Also usable without hardware : users can manually input feelings and session data.

**Needs to consider**:
- Offline playlist download
- Language-neutral interface
- Calm UI to match surfing mindset


## Data sources and AI methods

* Data:
  - Surf condition data from APIs like [MagicSeaweed](https://magicseaweed.com/developer/) or [Surfline](https://surflinelabs.com/)
  - Physiological data from wearables (HR, GPS, duration)
  - Spotify metadata (genre, tempo, energy)
  - User feedback on song/mood match (for continuous learning)

* AI Techniques:
  - Mood detection from biometric and surf data (clustering, classification)
  - Music recommendation (collaborative filtering, tempo-mood matching)
  - Reinforcement learning for adapting to feedback
 
## simply python mockup
```python
import random

moods = ["chill", "flow", "pumped", "exhausted"]
spotify_tracks = {
    "chill": ["Lo-fi Vibes", "Ocean Sounds", "Chillhop Essentials"],
    "flow": ["Indie Surf", "Groove Zone", "Surf Rock Mix"],
    "pumped": ["Surf Punk Energy", "Workout Beats", "Drum&Bass Ride"],
    "exhausted": ["Relax Piano", "Reggae Cool Down", "Acoustic Winddown"]
}

def suggest_playlist(session_duration, wave_height, heart_rate):
    mood = "flow"
    if heart_rate > 130 and wave_height > 1.5:
        mood = "pumped"
    elif session_duration > 60 and heart_rate < 110:
        mood = "exhausted"
    elif wave_height < 0.5:
        mood = "chill"
    playlist = random.choice(spotify_tracks[mood])
    print(f"Mood detected: {mood}\nSuggested playlist: {playlist}")

# Example session
suggest_playlist(session_duration=75, wave_height=1.2, heart_rate=105)
```

## Challenges

* Mood is subjective = AI might misinterpret emotions based on limited signals
* Not all users have wearables or accurate surf data.
* Spotify has API limits and availability constraints in some countries.
* Ethical consideration : avoiding over-reliance on biometric analysis.

## What next?

Future improvements could include:
- Integration with Apple Watch and Garmin surf profiles
- Use of voice input to describe mood
- Expansion to other sports (yoga, snowboarding)
- Adding generative music (AI-generated soundtracks)

Needed to move forward:
- A UX/UI designer
- Access to surf APIs
- Volunteers to test MVP (beta testers)
- More music data labeled by surfers

## Acknowledgments

- Inspired by the idea of "flow state" in surfing and sport psychology
- Music data from Spotify API – [Spotify Developer Docs](https://developer.spotify.com/)
- Surf data ideas inspired by [Surfline](https://www.surfline.com/) and [MSW](https://magicseaweed.com/)
- Mood detection ideas from the [Affectiva Emotion AI](https://www.smart-eye.com/emotion-ai/) concept
