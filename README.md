# social-media-research-agent
A research agent capable of doing social media research for a given product, service to help create relevant content.

## OpenDeepSearch Demo in Google Colab: Enhanced Search for AI Agents

This Google Colab notebook ods_agent_colab_demo.ipynp provides a hands-on demonstration of the OpenDeepSearch tool. OpenDeepSearch is designed to empower AI agents with advanced web search and information retrieval capabilities.
OpenDeepSearch is a lightweight yet powerful search tool optimized for integration with AI agents, particularly within ecosystems like Hugging Face's SmolAgents. 

### Setup
The sevices and the methods to get the keys has been mentioned here. These keys will be used in the Google Colab notebook file.
1. **Choose a Search Provider**:
   - **Option 1: Serper.dev**: Get **free 2500 credits** and add your API key.
     - Visit [serper.dev](https://serper.dev) to create an account.
     - Retrieve your API key
   - **Option 2: SearXNG**: Use a self-hosted or public SearXNG instance.
     - Specify the SearXNG instance URL when initializing OpenDeepSearch.
     - Optionally provide an API key if your instance requires authentication.

2. **Choose a Reranking Solution**:
   - **Quick Start with Jina**: Sign up at [Jina AI](https://jina.ai/) to get an API key for immediate use
   - **Self-hosted Option**: Set up [Infinity Embeddings](https://github.com/michaelfeil/infinity) server locally with open source models such as [Qwen2-7B-instruct](https://huggingface.co/Alibaba-NLP/gte-Qwen2-7B-instruct/tree/main)
   - For more details on reranking options, see our [Rerankers Guide](src/opendeepsearch/ranking_models/README.md)

3. **Set up LiteLLM Provider**:
   - Choose a provider from the [supported list](https://docs.litellm.ai/docs/providers/), including:
     - OpenAI
     - Anthropic
     - Google (Gemini)
     - OpenRouter
     - HuggingFace
     - Fireworks
     - And many more!
   - Set your chosen provider's API key as an environment variable:
   ```bash
   export <PROVIDER>_API_KEY='your-api-key-here'  # e.g., OPENAI_API_KEY, ANTHROPIC_API_KEY
   ```
   - For OpenAI, you can also set a custom base URL (useful for self-hosted endpoints or proxies):
   ```bash
   export OPENAI_BASE_URL='https://your-custom-openai-endpoint.com'
   ```
   - You can set default LiteLLM model IDs for different tasks:
   ```bash
   # General default model (fallback for all tasks)
   export LITELLM_MODEL_ID='openrouter/google/gemini-2.0-flash-001'

   # Task-specific models
   export LITELLM_SEARCH_MODEL_ID='openrouter/google/gemini-2.0-flash-001'  # For search tasks
   export LITELLM_ORCHESTRATOR_MODEL_ID='openrouter/google/gemini-2.0-flash-001'  # For agent orchestration
   export LITELLM_EVAL_MODEL_ID='gpt-4o-mini'  # For evaluation tasks
   ```
   - When initializing OpenDeepSearch, you can specify your chosen model using the provider's format (this will override the environment variables):
   ```python
   search_agent = OpenDeepSearchTool(model_name="provider/model-name")  # e.g., "anthropic/claude-3-opus-20240229", 'huggingface/microsoft/codebert-base', 'openrouter/google/gemini-2.0-flash-001'
   ```

### Features

This toolkit aims provides the following research features:

* **Market research:**
    AI enhances market surveys by:
    * Automating data aggregation.
    * Analyzing sentiment and trends.
    * Segmenting the market.
    * Predicting future trends.
    It provides reports on competitors, needs, market size, and SWOT, for efficient market analysis.

* **Augmenter:**
    * It goes beyond simply identifying keywords. It aims to capture the "voice" of the audience – their slang, idioms, common phrases, and even the emotional nuances they express.
    * By providing insights into audience voice, the Augmenter helps advertisers craft ad copy that feels more natural, authentic, and relatable to the audience. This can increase engagement and improve the effectiveness of advertising campaigns.
    * It reduces the time and guesswork involved in trying to "sound like" the target audience.

* **Audience Graph:**
    * It maps out how various groups within an audience are connected. For example, it might show that there's a significant overlap between "pet owners" and "parents," indicating that many people buy products for both their pets and their children.
    * The graph can reveal unexpected connections and dependencies within an audience, allowing advertisers to:
        * Identify cross-selling opportunities (e.g., promoting pet products to parents).
        * Tailor messaging to address the multiple roles and interests of individuals.
        * Understand how trends and behaviors in one segment might influence another.
    * It saves time by providing a quick and intuitive overview of audience relationships.

* **Habits:**
    This feature provides insights into the typical behaviors and preferences of a target audience.
    * It aims to give advertisers a comprehensive view of "a day in the life" of their audience. This includes:
        * **How they talk:** Their communication styles, language use, and online jargon.
        * **What they buy:** Their purchasing habits, product preferences, and brand affinities.
        * **What they do:** Their activities, hobbies, entertainment choices, and general lifestyle.
    * By understanding audience habits, advertisers can:
        * Choose the most effective channels and platforms for reaching them.
        * Develop ad creatives that align with their interests and routines.
        * Predict how they might respond to different marketing messages.
    * It saves time by consolidating information about audience behavior into a single, accessible resource.

* **Reddit Scanning:**
    This feature specifically analyzes discussions and content on the Reddit platform to gain deeper insights into audiences.
    * Reddit is a rich source of unfiltered opinions, discussions, and community interactions. This feature leverages that by:
        * Crawling and analyzing relevant Reddit threads and subreddits.
        * Identifying patterns in language, sentiment, and topics of conversation.
    * It helps advertisers understand:
        * Nuances in audience language and behavior that might not be apparent elsewhere.
        * Emerging trends and concerns within specific communities.
        * Authentic feedback on products, brands, and marketing campaigns.
    * It saves time by automating the process of sifting through large volumes of Reddit data.

* **Review Scanning:**
    This feature extracts and analyzes customer reviews from online platforms like Amazon and Shopify.
    * Customer reviews provide valuable insights into:
        * What customers like and dislike about products.
        * Their needs, pain points, and expectations.
        * The language they use to describe their experiences.
    * This feature helps advertisers:
        * Identify product strengths and weaknesses.
        * Understand customer sentiment and address concerns.
        * Refine messaging to highlight key benefits and features.
    * It saves time by automating the process of analyzing large numbers of reviews.

* **Audience Tracker:**

    This feature monitors specific events or timely trends that are relevant to a target audience.
    * It helps advertisers stay up-to-date with what's happening in their audience's lives, such as:
        * Seasonal events (e.g., holidays, back-to-school).
        * Cultural trends (e.g., viral challenges, memes).
        * Life events (e.g., weddings, graduations).
    * By tracking these events, advertisers can:
        * Create timely and relevant ad campaigns.
        * Anticipate changes in audience needs and behaviors.
        * Maximize the impact of their messaging.
    * It saves time by providing alerts and updates on important audience-related events.

* **AI CMO (Chief Marketing Officer):**
    This feature leverages AI to assist with high-level marketing strategy and planning.
    * It goes beyond tactical ad creation and helps with:
        * Market analysis.
        * Campaign planning.
        * Performance prediction.
        * Strategic recommendations.
    * It aims to provide CMO-level insights and guidance, helping marketing teams:
        * Make more informed decisions.
        * Optimize their overall marketing strategy.
        * Improve ROI.
    * It saves time and resources by automating complex analytical tasks and providing data-driven recommendations.

This notebook utilizes OpenDeepSearch, available at: https://github.com/sentient-agi/OpenDeepSearch/tree/main. We gratefully acknowledge the contributions of the OpenDeepSearch team.
