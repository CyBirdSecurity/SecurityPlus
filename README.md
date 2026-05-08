# Security+ SY0-701 Study Tool

An interactive web application for CompTIA Security+ exam preparation, built on the CyBird Security study tool framework.

## Features

- **5 Security+ Domains** aligned to the SY0-701 exam objectives
- **50 practice questions** (10 per domain) with detailed explanations
- **125 flashcards** (25 per domain) covering key terms and concepts
- **20 interactive questions** (4 per domain) — ordering, matching, multi-select, fill-in-the-blank
- Progress tracking with accuracy metrics and study streaks
- Focus Mode targeting your weakest domains
- Export/import progress as JSON

## Security+ SY0-701 Domains

| Domain | Name | Exam Weight |
|--------|------|-------------|
| 1 | General Security Concepts | 12% |
| 2 | Threats, Vulnerabilities, and Mitigations | 22% |
| 3 | Security Architecture | 18% |
| 4 | Security Operations | 28% |
| 5 | Security Program Management and Oversight | 20% |

## Usage

Open `index.html` in a browser. The app loads YAML data files via `fetch()` so it requires either:
- A local web server: `python3 -m http.server 8080` then visit `http://localhost:8080`
- A static hosting service (GitHub Pages, Netlify, Vercel)

## Project Structure

```
├── index.html              # Single-page application shell
├── cert.config.js          # Certification-specific config (name, labels, etc.)
├── data/
│   ├── domains.yml         # Domain definitions with weights and colors
│   ├── questions/          # 10 multiple-choice questions per domain
│   ├── flashcards/         # 25 flashcards per domain
│   └── interactive/        # 4 interactive questions per domain
├── assets/
│   ├── app.js              # Main app entrypoint and routing
│   └── styles.css          # Dark-theme stylesheet
├── components/
│   ├── quiz.js             # Quiz component (setup → active → results → review)
│   ├── flashcard.js        # Flashcard study component
│   ├── feedback.js         # Answer feedback renderer
│   └── interactive.js      # Interactive question types renderer
├── utils/
│   ├── loader.js           # YAML file fetcher with caching
│   ├── quizEngine.js       # Question selection, scoring, and analysis
│   ├── progress.js         # localStorage-based progress tracking
│   └── validator.js        # Data validation
└── tests/
    └── validate.js         # Node.js data validation test suite
```

## Adding Content

To add more questions or flashcards, follow the YAML schema in each file:

**Question format** (`data/questions/domainN.yml`):
```yaml
questions:
  - id: q-dN-XXX
    domain: domainN
    question: "Question text?"
    options:
      - "A. Option one"
      - "B. Option two"
      - "C. Option three"
      - "D. Option four"
    correct_answer: 0  # 0-indexed
    explanations:
      correct: "Why this answer is correct."
      incorrect:
        - null         # skip the correct one
        - "Why B is wrong."
        - "Why C is wrong."
        - "Why D is wrong."
    tags: [tag1, tag2]
    difficulty: easy|medium|hard
```

**Flashcard format** (`data/flashcards/domainN.yml`):
```yaml
flashcards:
  - id: fc-dN-XXX
    domain: domainN
    term: "Term or acronym"
    definition: "Complete definition."
    tags: [tag1, tag2]
```

## Running Tests

```bash
npm install
npm test
```

## Adapting for Another Certification

1. Update `cert.config.js` with the new certification name and labels
2. Replace `data/domains.yml` with the new exam domains
3. Replace all files in `data/questions/`, `data/flashcards/`, and `data/interactive/`
4. Update the domain count in `tests/validate.js`

## License

MIT — Based on the [CyBirdSecurity/CISSP](https://github.com/CyBirdSecurity/CISSP) framework.
