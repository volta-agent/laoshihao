# Laoshihao 老师好 - Chinese Learning Platform

Chinese learning platform based on HSK courses for English speakers.

## Live Demo

🌐 **Live Site**: https://volta-agent.github.io/laoshihao/

## Features

- **HSK-Aligned Content**: Structured according to official HSK levels 1-5
- **Interactive Learning**: Vocabulary, dialogues, and grammar exercises
- **Text-to-Speech**: Browser-based pronunciation for accurate Chinese tones
- **Responsive Design**: Works on desktop, tablet, and mobile
- **Gamified Learning**: Flashcard-style vocabulary practice
- **Comprehensive Content**: 40+ HSK 1 words with more to come

## Tech Stack

- **Framework**: Svelte 5 with runes ($state, $derived, $effect)
- **Build Tool**: Vite
- **Styling**: CSS with Gruvbox Dark theme
- **Deployment**: GitHub Pages
- **Data**: JSON files for vocabulary, dialogues, and grammar

## Project Structure

```
src/
├── lib/
│   ├── data/
│   │   ├── vocabulary/    # hsk1.json, hsk2.json, etc.
│   │   ├── dialogues/     # hsk1_dialogues.json, etc.
│   │   └── grammar/       # hsk1_grammar.json, etc.
├── App.svelte            # Main application component
├── main.ts              # Entry point
└── app.css              # Global styles
```

## Getting Started

### Local Development

```bash
# Clone the repository
git clone https://github.com/volta-agent/laoshihao.git
cd laoshihao

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

### Deployment

The site is automatically deployed to GitHub Pages using the `gh-pages` branch. To manually deploy:

```bash
npm run build
npx gh-pages -d dist -b gh-pages --dotfiles
```

## Content Structure

### Vocabulary
Each HSK level has a JSON file with:
```json
{
  "hanzi": "你好",
  "pinyin": "nǐ hǎo",
  "english": "hello",
  "pos": "interjection",
  "hsk_level": 1,
  "tags": ["greeting", "basic"]
}
```

### Dialogues
Interactive conversations with Chinese, pinyin, and English translations.

### Grammar
Grammar points with explanations, structures, and examples.

## Roadmap

- [x] Basic HSK 1 vocabulary (40 words)
- [x] Dialogues for all HSK levels
- [x] Grammar points for all HSK levels
- [x] Responsive UI with Gruvbox theme
- [x] Text-to-speech pronunciation
- [x] GitHub Pages deployment
- [ ] Complete HSK 1-5 vocabulary (3000+ words)
- [ ] Quiz system with scoring
- [ ] Progress tracking with localStorage
- [ ] Spaced repetition flashcards
- [ ] Audio recordings for dialogues
- [ ] Mobile app with PWA support

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add your content (vocabulary, dialogues, grammar)
4. Submit a pull request

## License

MIT License - see LICENSE file for details

## Acknowledgements

- HSK (汉语水平考试) curriculum materials
- Svelte team for the amazing framework
- Vite for fast builds
- GitHub for free hosting