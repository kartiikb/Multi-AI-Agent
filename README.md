# Reddit AI Blog Generator with CrewAI

🚀 A Python script that scrapes AI-related content from Reddit and generates a technical blog article using AI agents powered by CrewAI and local LLMs via Ollama.

## Features

- **Reddit Scraping**: Pulls latest posts/comments from r/LocalLLaMA
- **Multi-Agent Workflow**: Uses 3 specialized AI agents (Researcher, Writer, Critic)
- **Local LLM Support**: Default configuration uses Mistral via Ollama
- **Human-in-the-Loop**: Allows for human feedback during the process
- **Markdown Formatting**: Outputs professionally formatted blog posts

## Requirements

1. Python 3.9+
2. Reddit API credentials (create app at [Reddit Apps](https://www.reddit.com/prefs/apps))
3. Ollama installed (for local LLM) - [Install Guide](https://ollama.ai/)
4. OpenAI API key (optional for GPT-4)

## Setup

1. **Install dependencies**
```bash
pip install praw langchain crewai python-dotenv ollama
```

2. **Environment Variables**
Create `.env` file:
```ini
REDDIT_CLIENT_ID=your_client_id
REDDIT_CLIENT_SECRET=your_client_secret
REDDIT_USER_AGENT=your_user_agent
OPENAI_API_KEY=your_openai_key  # Optional
```

3. **Ollama Setup** (for local models)
```bash
ollama pull mistral
```

## Usage

```python
python reddit_blog_generator.py
```

The script will:
1. Scrape recent r/LocalLLaMA posts
2. Generate analysis report
3. Create blog draft
4. Provide editorial feedback
5. Output final markdown-formatted blog

## Code Structure

### Key Components

1. **BrowserTool** - Custom Reddit scraper
   - Scrapes posts and comments
   - Handles API rate limits
   - Returns structured data

2. **AI Agents**
   - **Explorer**: Researches trending AI projects
   - **Writer**: Creates engaging technical content
   - **Critic**: Ensures quality and clarity

3. **Task Pipeline**
   - Sequential processing of research → writing → editing

### Agent Configuration

```python
explorer = Agent(
    role="Senior Researcher",
    tools=[BrowserTool().scrape_reddit] + human_tools,
    llm=mistral  # Can replace with GPT-4
)
```

### Customization Options

1. **Switch LLMs**
   - For GPT-4: Remove `llm=mistral` and set OpenAI key
   - Try other Ollama models: `llama2`, `codellama`

2. **Adjust Scraping**
```python
# Modify in BrowserTool class
subreddit.hot(limit=12)  # Change limit/post count
comments = comments[:7]  # Comments per post
```

3. **Change Output Format**
```python
# In task_blog description modify:
"## [Title](link)"  # Markdown template
```

## Example Output

```markdown
## [LM Studio](https://lmstudio.ai/)
- New local LLM runner with GPU acceleration
- Enables running 70B models on consumer hardware
- Makes private AI development accessible

## [OpenVoice](https://github.com/myshell-ai/OpenVoice)
- Instant voice cloning technology
- Supports real-time emotion control
- Opens new possibilities for voice interfaces
...
```

## Contribution

Feel free to:
- Add new scraping sources
- Implement better error handling
- Enhance formatting templates
- Add PDF/HTML export features

---

**Note:** Always respect Reddit's API terms of service. This is a demo - consider adding rate limiting and proper error handling for production use.
