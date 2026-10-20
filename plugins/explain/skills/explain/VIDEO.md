# L4 - Explainer video (3b1b style)

The output is a narrated `.mp4` file. Manim makes the animation. Text-to-speech makes the narration. Manim puts the audio into the video, so you do not need a separate mux step.

## 1. Check the tools

```bash
for b in manim ffmpeg ffprobe; do command -v $b >/dev/null || echo "missing: $b"; done
[ -n "$ELEVENLABS_API_KEY" ] && echo "tts: elevenlabs" || { command -v say >/dev/null && echo "tts: say" || echo "missing: tts"; }
command -v latex >/dev/null || echo "no latex: use Text/MarkupText, not Tex/MathTex"
```

When a tool is missing, stop and give the user the install commands:
- macOS: `brew install ffmpeg cairo pango pkg-config && uv tool install manim`
- LaTeX (only for real math typesetting): `brew install --cask mactex-no-gui`
- Better narration: set `ELEVENLABS_API_KEY` (optional: `ELEVENLABS_VOICE_ID`).

## 2. Write the script

Work dir: `${TMPDIR:-/tmp}/explain/<slug>/`.

1. Make 3-6 beats. One beat = one idea = one narration paragraph plus the animation that shows it. Total length 1-3 minutes, unless the user asks for a different length.
2. Write the narration in soft STE ([STE.md](STE.md)). Write for the ear: short sentences, no symbols that a voice cannot read, numbers written the way they are spoken.
3. Plan the visual for each beat before you write code. Show, then name: the shape appears first, then the label or the narration explains it.

## 3. Make the narration audio, one file per beat

ElevenLabs (when the key is set):

```bash
curl -sS -X POST "https://api.elevenlabs.io/v1/text-to-speech/${ELEVENLABS_VOICE_ID:-21m00Tcm4TlvDq8ikWAM}" \
  -H "xi-api-key: $ELEVENLABS_API_KEY" -H "Content-Type: application/json" \
  -d "$(jq -n --arg t "$TEXT" '{text:$t, model_id:"eleven_multilingual_v2"}')" -o beat1.mp3
```

macOS fallback (local, free):

```bash
say -o beat1.aiff "$TEXT" && ffmpeg -loglevel error -y -i beat1.aiff beat1.wav
```

Tell the user which voice source you used.

## 4. Write the scene

Each beat plays its audio, runs its animations, then waits until the audio ends. The animation length follows the narration length.

```python
from manim import *
import subprocess

def duration(path):
    return float(subprocess.check_output(
        ["ffprobe", "-v", "error", "-show_entries", "format=duration", "-of", "csv=p=0", path]))

class Explainer(Scene):
    def beat(self, audio, animate):
        start = self.renderer.time
        self.add_sound(audio)
        animate()
        left = duration(audio) - (self.renderer.time - start)
        self.wait(max(left, 0) + 0.4)

    def construct(self):
        title = Text("Exponential backoff", font_size=56)
        self.beat("beat1.wav", lambda: self.play(Write(title), run_time=1.5))
        # next beats: self.beat("beat2.wav", lambda: ...)
```

Style (3b1b look):
- Dark background (the Manim default), few colors, one accent color for the focus element.
- Move and transform objects (`Transform`, `ReplacementTransform`, `animate`) so the viewer can follow one object from step to step. Do not cut to a new frame.
- Keep 1-3 main objects on screen. Remove old objects with `FadeOut` before you add new ones.
- Use `Text` for labels. Use `MathTex` only when `latex` is installed.

## 5. Render and check

```bash
manim -ql scene.py Explainer --media_dir media   # fast draft, 480p15
manim -qh scene.py Explainer --media_dir media   # final, 1080p60
```

Output: `media/videos/scene/<quality>/Explainer.mp4`.

Check the draft before you render the final video:
1. `ffprobe` shows one video stream and one audio stream, and the duration is close to the total narration length.
2. Look at frames from each beat (for example, read the `.mp4` file at a timestamp). Text must not overlap, leave the frame, or stay on screen after its beat.
3. Fix the problems, render the final video, and run `open` on it.
