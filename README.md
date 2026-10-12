# Documentary Agent Kit — "One sentence → YouTube-ready video"

A ready-to-install AGENTS.md + 8 stage Skills + 2 subagents that fuse your existing repos (ai-documentary-studio, ytagent, babymonster-documentary-pipeline, vfactory) with the strongest open stack (OpenMontage → HyperFrames → edge-tts → faster-whisper → FFmpeg → YouTube Data API).

## Install (30 seconds)

```bash
# 1. Copy the kit anywhere your coding agent can open
cp -r documentary-agent-kit ~/documentary-studio && cd ~/documentary-studio

# 2. Make it visible to your agent
ln -s AGENTS.md CLAUDE.md            # Claude Code (or just open the folder in Cursor/Codex/Cline — they read AGENTS.md natively)

# 3. One-time deps
ffmpeg -version && node -v           # need FFmpeg + Node 22+
pip install edge-tts faster-whisper yt-dlp pillow google-api-python-client google-auth-oauthlib
npx skills add heygen-com/hyperframes   # render engine + 21 bonus video skills

# 4. Optional keys in .env (pipeline runs FREE without them)
#    PEXELS_API_KEY, PIXABAY_API_KEY, ELEVENLABS_API_KEY, YOUTUBE_CLIENT_SECRET_JSON
```

## Run

Say to your agent:

> **build a documentary on ahyeon using examples/ahyeon-dossier.md**

The agent executes S0→S8 (intent → research → script → media → voiceover → timeline → captions/thumbnail → render/QC → publish-unlisted). Artifacts land in `documentary/ahyeon/`. You approve the script (S2) and the QC report (S7), then flip the video public. Add "fully automatic" to skip the approval pauses.

Any other topic works the same — the research skill rebuilds the dossier from Wikipedia/web when no dossier is supplied.

## Files

```text
AGENTS.md                        ← the orchestrator contract (drop-in)
skills/research-facts/SKILL.md   ← S1 Wikipedia/Wikidata/web → sourced facts
skills/write-script/SKILL.md     ← S2 facts → script JSON (hook/acts/beats)
skills/source-media/SKILL.md     ← S3 Pexels/Pixabay/Commons/IA/NASA + ytagent
skills/gen-voiceover/SKILL.md    ← S4 edge-tts → ElevenLabs → kokoro ladder
skills/assemble-timeline/SKILL.md← S5 EDL JSON (Ken Burns, cards, ducked music)
skills/captions-meta/SKILL.md    ← S6 ASS karaoke captions + thumbnail + SEO
skills/render-qc/SKILL.md        ← S7 segment render → concat → QC battery
skills/publish-youtube/SKILL.md  ← S8 resumable upload, unlisted by default
.claude/agents/fact-researcher.md ← subagent: token-heavy research fan-out
.claude/agents/media-scout.md     ← subagent: rate-limit-safe media fan-out
examples/ahyeon-dossier.md        ← verified fact pack for your first run
```

## Upgrade path

When you want archival-heavy, real-footage productions beyond this kit's scope: clone `calesthio/OpenMontage` (65.7k★) and run its `documentary-montage` pipeline — feed it the same dossier as the research seed. Render engine alternatives and the full repo catalog live in `../github-repos-catalog.md`; architecture deep-dive in `../documentary-agent-blueprint.md`.
