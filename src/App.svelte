<script>
  import hsk1 from './lib/data/vocabulary/hsk1.json';
  import hsk2 from './lib/data/vocabulary/hsk2.json';
  import hsk3 from './lib/data/vocabulary/hsk3.json';
  import hsk4 from './lib/data/vocabulary/hsk4.json';
  import hsk5 from './lib/data/vocabulary/hsk5.json';
  
  import hsk1Dialogues from './lib/data/dialogues/hsk1_dialogues.json';
  import hsk2Dialogues from './lib/data/dialogues/hsk2_dialogues.json';
  import hsk3Dialogues from './lib/data/dialogues/hsk3_dialogues.json';
  import hsk4Dialogues from './lib/data/dialogues/hsk4_dialogues.json';
  import hsk5Dialogues from './lib/data/dialogues/hsk5_dialogues.json';
  
  import hsk1Grammar from './lib/data/grammar/hsk1_grammar.json';
  import hsk2Grammar from './lib/data/grammar/hsk2_grammar.json';
  import hsk3Grammar from './lib/data/grammar/hsk3_grammar.json';
  import hsk4Grammar from './lib/data/grammar/hsk4_grammar.json';
  import hsk5Grammar from './lib/data/grammar/hsk5_grammar.json';
  
  let currentView = 'home';
  let selectedLevel = 1;
  
  const HSK_DATA = {
    1: hsk1,
    2: hsk2,
    3: hsk3,
    4: hsk4,
    5: hsk5
  };
  
  const DIALOGUE_DATA = {
    1: hsk1Dialogues,
    2: hsk2Dialogues,
    3: hsk3Dialogues,
    4: hsk4Dialogues,
    5: hsk5Dialogues
  };
  
  const GRAMMAR_DATA = {
    1: hsk1Grammar,
    2: hsk2Grammar,
    3: hsk3Grammar,
    4: hsk4Grammar,
    5: hsk5Grammar
  };
  
  const LEVELS = [
    { level: 1, name: 'HSK 1', count: hsk1.length, desc: 'Beginner' },
    { level: 2, name: 'HSK 2', count: hsk2.length, desc: 'Elementary' },
    { level: 3, name: 'HSK 3', count: hsk3.length, desc: 'Intermediate' },
    { level: 4, name: 'HSK 4', count: hsk4.length, desc: 'Upper Intermediate' },
    { level: 5, name: 'HSK 5', count: hsk5.length, desc: 'Advanced' }
  ];
  
  function speakChinese(text) {
    if ('speechSynthesis' in window) {
      const utter = new SpeechSynthesisUtterance(text);
      utter.lang = 'zh-CN';
      utter.rate = 0.9;
      speechSynthesis.speak(utter);
    } else {
      alert('Speech synthesis not supported in your browser');
    }
  }
</script>

<nav class="navbar">
  <div class="nav-brand">Laoshihao 老师好</div>
  <div class="nav-links">
    <button class="nav-link {currentView === 'home' ? 'active' : ''}" onclick={() => currentView = 'home'}>Home</button>
    <button class="nav-link {currentView === 'vocabulary' ? 'active' : ''}" onclick={() => currentView = 'vocabulary'}>Vocabulary</button>
    <button class="nav-link {currentView === 'dialogues' ? 'active' : ''}" onclick={() => currentView = 'dialogues'}>Dialogues</button>
    <button class="nav-link {currentView === 'grammar' ? 'active' : ''}" onclick={() => currentView = 'grammar'}>Grammar</button>
    <button class="nav-link {currentView === 'quiz' ? 'active' : ''}" onclick={() => currentView = 'quiz'}>Quiz</button>
  </div>
</nav>

<main>
  {#if currentView === 'home'}
    <section class="hero">
      <h1>Laoshihao - Chinese Learning Platform</h1>
      <p class="subtitle">Master Chinese with HSK-aligned courses for English speakers</p>
      
      <div class="level-grid">
        {#each LEVELS as level}
          <div class="level-card">
            <h3>{level.name}</h3>
            <p>{level.desc}</p>
            <div class="stats">
              <span class="stat">{level.count} words</span>
              <span class="stat">10 dialogues</span>
              <span class="stat">5 grammar points</span>
            </div>
            <button class="start-button" onclick={() => { selectedLevel = level.level; currentView = 'vocabulary'; }}>Start Learning →</button>
          </div>
        {/each}
      </div>
      
      <div class="features">
        <h2>Platform Features</h2>
        <div class="feature-grid">
          <div class="feature">
            <h3>🎯 HSK-Aligned</h3>
            <p>Structured according to official HSK levels 1-5</p>
          </div>
          <div class="feature">
            <h3>🗣️ Pronunciation</h3>
            <p>Text-to-speech for accurate Chinese pronunciation</p>
          </div>
          <div class="feature">
            <h3>📚 Comprehensive</h3>
            <p>Vocabulary, dialogues, grammar, and quizzes</p>
          </div>
          <div class="feature">
            <h3>📱 Responsive</h3>
            <p>Works on desktop, tablet, and mobile</p>
          </div>
        </div>
      </div>
    </section>
    
  {:else if currentView === 'vocabulary'}
    <section class="vocabulary-section">
      <div class="section-header">
        <h2>HSK {selectedLevel} Vocabulary</h2>
        <div class="level-selector">
          {#each LEVELS as level}
            <button class="level-tab {selectedLevel === level.level ? 'active' : ''}" onclick={() => selectedLevel = level.level}>
              {level.name}
            </button>
          {/each}
        </div>
      </div>
      
      <div class="vocabulary-list">
        {#each HSK_DATA[selectedLevel] as word}
          <div class="vocab-card">
            <div class="vocab-hanzi">{word.hanzi}</div>
            <div class="vocab-pinyin">{word.pinyin}</div>
            <div class="vocab-english">{word.english}</div>
            <div class="vocab-details">
              <span class="pos-tag">{word.pos}</span>
              {#each word.tags as tag}
                <span class="word-tag">{tag}</span>
              {/each}
            </div>
            <button class="speak-button" onclick={() => speakChinese(word.hanzi)}>🔊 Speak</button>
          </div>
        {/each}
      </div>
    </section>
    
  {:else if currentView === 'dialogues'}
    <section class="dialogues-section">
      <div class="section-header">
        <h2>HSK {selectedLevel} Dialogues</h2>
        <div class="level-selector">
          {#each LEVELS as level}
            <button class="level-tab {selectedLevel === level.level ? 'active' : ''}" onclick={() => selectedLevel = level.level}>
              {level.name}
            </button>
          {/each}
        </div>
      </div>
      
      {#each DIALOGUE_DATA[selectedLevel] as dialogue}
        <div class="dialogue-card">
          <h3>{dialogue.title}</h3>
          <div class="dialogue-lines">
            {#each dialogue.lines as line}
              <div class="dialogue-line">
                <div class="speaker">{line.speaker}:</div>
                <div class="chinese">{line.chinese}</div>
                <div class="pinyin">{line.pinyin}</div>
                <div class="english">{line.english}</div>
                <button class="speak-line" onclick={() => speakChinese(line.chinese)}>🔊</button>
              </div>
            {/each}
          </div>
        </div>
      {/each}
    </section>
    
  {:else if currentView === 'grammar'}
    <section class="grammar-section">
      <div class="section-header">
        <h2>HSK {selectedLevel} Grammar</h2>
        <div class="level-selector">
          {#each LEVELS as level}
            <button class="level-tab {selectedLevel === level.level ? 'active' : ''}" onclick={() => selectedLevel = level.level}>
              {level.name}
            </button>
          {/each}
        </div>
      </div>
      
      {#each GRAMMAR_DATA[selectedLevel] as grammar}
        <div class="grammar-card">
          <h3>{grammar.title}</h3>
          <div class="grammar-category">{grammar.category}</div>
          <p class="grammar-explanation">{grammar.explanation}</p>
          <div class="grammar-structure">{grammar.structure}</div>
          <div class="grammar-examples">
            <h4>Examples:</h4>
            {#each grammar.examples as example}
              <div class="example">
                <div class="chinese">{example.chinese}</div>
                <div class="pinyin">{example.pinyin}</div>
                <div class="english">{example.english}</div>
              </div>
            {/each}
          </div>
        </div>
      {/each}
    </section>
    
  {:else if currentView === 'quiz'}
    <section class="quiz-section">
      <h2>Test Your Knowledge</h2>
      <div class="level-buttons">
        {#each LEVELS as level}
          <button class="level-card" onclick={() => startQuiz(level.level)}>
            <div class="level-code">📝</div>
            <div class="level-name">{level.name} Quiz</div>
            <div class="level-desc">Test 10 {level.name} words</div>
            <div class="level-action">Start →</div>
          </button>
        {/each}
      </div>
    </section>
  {/if}
</main>

<style>
  .navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    background-color: var(--c-dark-secondary);
    border-bottom: 2px solid var(--c-med-purple);
  }
  
  .nav-brand {
    font-size: 24px;
    font-weight: bold;
    color: var(--c-text-primary);
  }
  
  .nav-links {
    display: flex;
    gap: 15px;
  }
  
  .nav-link {
    background: none;
    border: none;
    color: var(--c-text-secondary);
    font-size: 16px;
    cursor: pointer;
    padding: 8px 16px;
    border-radius: 5px;
    transition: all 0.2s;
  }
  
  .nav-link:hover, .nav-link.active {
    background-color: var(--c-med-purple);
    color: white;
  }
  
  .hero {
    text-align: center;
    padding: 40px 20px;
  }
  
  .hero h1 {
    font-size: 2.5rem;
    margin-bottom: 10px;
  }
  
  .subtitle {
    font-size: 1.2rem;
    color: var(--c-text-secondary);
    margin-bottom: 40px;
  }
  
  .level-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 25px;
    margin: 40px 0;
  }
  
  .level-card {
    background-color: var(--c-dark-secondary);
    border-radius: 10px;
    padding: 25px;
    text-align: left;
    transition: transform 0.2s;
  }
  
  .level-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  }
  
  .level-card h3 {
    margin-top: 0;
    color: var(--c-text-primary);
  }
  
  .stats {
    display: flex;
    gap: 15px;
    margin: 15px 0;
    font-size: 14px;
  }
  
  .stat {
    background-color: var(--c-dark-accent);
    padding: 5px 10px;
    border-radius: 15px;
  }
  
  .start-button {
    width: 100%;
    margin-top: 15px;
  }
  
  .features {
    margin-top: 60px;
  }
  
  .feature-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 25px;
    margin-top: 30px;
  }
  
  .feature {
    padding: 20px;
    background-color: var(--c-dark-secondary);
    border-radius: 8px;
  }
  
  .feature h3 {
    margin-top: 0;
  }
  
  .section-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30px;
    flex-wrap: wrap;
    gap: 15px;
  }
  
  .level-selector {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
  }
  
  .level-tab {
    background-color: var(--c-dark-secondary);
    border: none;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
    transition: all 0.2s;
  }
  
  .level-tab:hover, .level-tab.active {
    background-color: var(--c-med-purple);
    color: white;
  }
  
  .vocabulary-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 20px;
  }
  
  .vocab-card {
    background-color: var(--c-dark-secondary);
    border-radius: 8px;
    padding: 20px;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  
  .vocab-hanzi {
    font-size: 2rem;
    font-weight: bold;
  }
  
  .vocab-pinyin {
    color: var(--c-text-secondary);
    font-size: 1.2rem;
  }
  
  .vocab-english {
    font-size: 1.1rem;
    margin: 10px 0;
  }
  
  .vocab-details {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
  }
  
  .pos-tag {
    background-color: var(--c-success);
    color: white;
    padding: 3px 8px;
    border-radius: 12px;
    font-size: 12px;
  }
  
  .word-tag {
    background-color: var(--c-dark-accent);
    padding: 3px 8px;
    border-radius: 12px;
    font-size: 12px;
  }
  
  .speak-button {
    align-self: flex-start;
    padding: 8px 15px;
    font-size: 14px;
  }
  
  .dialogue-card {
    background-color: var(--c-dark-secondary);
    border-radius: 8px;
    padding: 25px;
    margin-bottom: 25px;
  }
  
  .dialogue-lines {
    display: flex;
    flex-direction: column;
    gap: 15px;
    margin-top: 20px;
  }
  
  .dialogue-line {
    display: grid;
    grid-template-columns: 50px 1fr auto auto;
    gap: 15px;
    align-items: center;
    padding: 10px;
    background-color: var(--c-dark-accent);
    border-radius: 5px;
  }
  
  .speaker {
    font-weight: bold;
  }
  
  .speak-line {
    background: none;
    border: none;
    cursor: pointer;
    font-size: 18px;
  }
  
  .grammar-card {
    background-color: var(--c-dark-secondary);
    border-radius: 8px;
    padding: 25px;
    margin-bottom: 25px;
  }
  
  .grammar-category {
    background-color: var(--c-dark-accent);
    padding: 5px 10px;
    border-radius: 15px;
    display: inline-block;
    margin-bottom: 15px;
  }
  
  .grammar-structure {
    font-family: monospace;
    background-color: var(--c-dark-primary);
    padding: 15px;
    border-radius: 5px;
    margin: 15px 0;
    border-left: 3px solid var(--c-med-purple);
  }
  
  .example {
    margin: 10px 0;
    padding: 10px;
    background-color: var(--c-dark-accent);
    border-radius: 5px;
  }
  
  .quiz-section {
    padding: 30px;
  }
  
  .level-buttons {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 25px;
    margin-top: 30px;
  }
  
  @media (max-width: 768px) {
    .navbar {
      flex-direction: column;
      gap: 15px;
    }
    
    .nav-links {
      flex-wrap: wrap;
      justify-content: center;
    }
    
    .section-header {
      flex-direction: column;
      align-items: flex-start;
    }
    
    .dialogue-line {
      grid-template-columns: 1fr;
      gap: 5px;
    }
  }
</style>