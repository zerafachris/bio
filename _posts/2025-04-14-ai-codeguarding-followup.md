---
title: "Crafting CodeGuardian: My Journey with LLMs and Prompt Engineering for Kaggle Competitions"
tags:
  - AI
  - LLM
  - Software Engineering
  - Prompt Engineering
  - Future of Work
  - Agentic AI
  - Code Quality Assurance
  - Automated Testing
  - Retrieval Augmented Generation
  - Software Development
  - Prompt Engineering
  - Kaggle Competitions
  - AI-Assisted Coding
toc: true
---

<figure>
	<a href=""><img src="https://i.imgur.com/lgMBvG3.png"></a>
</figure>

When I embarked on creating CodeGuardian for the [Kaggle Gen AI Intensive Course Capstone 2025Q1](https://www.kaggle.com/competitions/gen-ai-intensive-course-capstone-2025q1/overview), I knew that leveraging the power of Large Language Models (LLMs) would be essential. The competition challenged participants to develop innovative AI solutions, and I chose to focus on solving quality assurance challenges in code deployments through agentic AI. What made this project particularly interesting was my approach to development—I used prompt engineering techniques to guide LLMs in generating the foundation of my submission.

## The Power of Prompt Engineering in AI Development

Prompt engineering has emerged as a critical skill in the AI era. As described by Elvis Saravia's comprehensive guide, it's "a relatively new discipline for developing and optimising prompts to efficiently use language models for a wide variety of applications"[^4]. For my Kaggle submission, I needed to craft prompts that would generate high-quality, functional code while providing the creative direction for my project.

The process wasn't simply about asking an AI to "write code." Instead, it required careful consideration of prompt structure, specificity, and context to guide the model toward producing useful outputs that I could then refine and enhance.

## My Three-Pronged Prompt Strategy

My approach involved three distinct prompts, each serving a specific purpose in my development workflow:

### 1. The Main Code Base Prompt

The foundation of my project began with a carefully crafted prompt that set the stage for the entire codebase:

```
Act as a grand master kaggler from www.kaggle.com.

Think before you reply, be creative. Come up with a proposal submission for the competition https://www.kaggle.com/competitions/gen-ai-intensive-course-capstone-2025q1. In particular, the project to be considered should try and solve quality assurance in code deployments via agentic AI.

Provide me the submission for the competition
```

This prompt exemplifies several best practices in prompt engineering. First, it establishes a clear role for the AI to assume—that of a "grand master kaggler"—which is an example of role prompting[^10]. This technique helps frame the AI's perspective and expertise level. Second, it provides specific context about the competition and the problem domain (quality assurance in code deployments), giving the model clear boundaries for its response.

The instruction to "think before you reply, be creative" encourages the model to generate more thoughtful and innovative solutions rather than rushing to a standard answer—a technique that aligns with the "give the model room to think" best practice identified by PromptHub[^7].

### 2. The Blog Article Prompt

For documenting my project, I needed a comprehensive article that would explain my approach in a professional manner:

```
I want you to act as a professional tech blogger. Write an article for my professional website. The article must be accurate, professional, written in British English, and informative. It will be written in markdown. Take your time to think, and digest the information available, both in the provided resources and on the web to come up with a very good knowledgeable content. The article is about my submission to the Kaggle Gen AI Intensive Course Capstone 2025Q1 (https://www.kaggle.com/competitions/gen-ai-intensive-course-capstone-2025q1). My submission to the competition is CodeGuarding, an Agentic AI for Autonomous Code Quality Assurance. here is my code :

{CODE}

Provide a prompt to give to an LLM to draw an image for this article. The image aspect ratio should be 16:9.

Also provide 5 keywords or tags associated with this article
```

This prompt demonstrates several advanced techniques. It uses clear formatting requirements (markdown) and style specifications (British English, professional tone), which follows the "clarify the format" best practice[^7]. The instruction to "take your time to think, and digest the information" is a form of chain-of-thought prompting, encouraging the model to process information more thoroughly before generating content[^5].

By including my actual code in the prompt (represented by `{CODE}` in my summary), I provided the model with crucial context—a technique that Google Cloud identifies as "providing context and background information"[^12]. This allowed the model to generate an article that accurately reflected my implementation details.

### 3. The Video Script Prompt

For creating a promotional video script, I used a highly structured prompt that broke down the content into timed sections:

```
Create a 2-minute explainer video for CodeGuardian, an innovative AI-powered code quality assurance tool designed for software development teams. The video should target software engineers, QA professionals, and tech leaders in a professional yet engaging tone. Use a combination of animated graphics, code snippets, and a voiceover to convey the following key points:

1. Introduction (15 seconds):
   - Brief overview of the challenges in modern software development (rapid deployments, code quality issues)
   - Introduce CodeGuardian as an AI-powered solution

2. Key Features (60 seconds):
   - Intelligent Code Analysis: Show how CodeGuardian uses advanced AI to identify potential bugs, security vulnerabilities, and code smells
   - Automated Test Generation: Demonstrate the tool generating comprehensive test cases based on code changes
   - Real-time Fixes: Visualise how CodeGuardian suggests and implements code improvements
   - Cross-platform Compatibility: Highlight its ability to work with various programming languages and frameworks

3. Technology Behind CodeGuardian (20 seconds):
   - Briefly explain the use of FAISS vector store for efficient code similarity search
   - Mention the integration with Google's advanced text-embedding-004 model
   - Show a simplified visualisation of how the AI processes and understands code

4. Benefits for Development Teams (15 seconds):
   - Faster development cycles
   - Improved code quality
   - Reduced manual QA effort
   - Enhanced security

5. Call to Action (10 seconds):
   - Invite viewers to try CodeGuardian with a free trial
   - Direct them to the website for more information

Throughout the video:
- Use a clean, modern design with a color scheme of blue, white, and gray to convey professionalism and innovation
- Include animated code snippets that showcase before and after scenarios of code improvement
- Use smooth transitions between sections
- Add subtle background music that conveys a sense of technological advancement
- Include captions for accessibility

End the video with a tagline: 'CodeGuardian: Elevating Code Quality with AI-Powered Precision'
```

This prompt exemplifies the "split complex tasks into simpler subtasks" technique recommended by OpenAI[^9]. By breaking the video into five distinct sections with specific timing allocations, I made it easier for the AI to generate a well-structured script that covered all necessary aspects of my project.

The prompt also specifies the target audience, tone, and visual elements, providing comprehensive guidance that constrains the model's output in productive ways. This aligns with TechTarget's recommendation to "make clear, specific requests"[^11].

## Refining and Iterating on AI-Generated Content

While these prompts provided excellent starting points, the development process wasn't simply a matter of accepting the AI's output verbatim. As noted in the Kaggle competition on LLM taming, "the key to putting together a good solution is to know which techniques could be most relevant to the task at hand"[^1].

After receiving initial outputs from my prompts, I went through several iterations of refinement:

1. **Code Evaluation and Enhancement**: I analysed the generated code for functionality, efficiency, and alignment with competition requirements. This involved testing different components, identifying limitations, and making necessary modifications.
2. **Content Integration**: For the blog article, I needed to ensure that the AI-generated content accurately reflected my actual implementation while maintaining a professional tone and comprehensive coverage of the topic.
3. **Visual Script Adaptation**: The video script required adjustments to ensure it would translate effectively to the InVideo platform, with appropriate timing and visual cues.

This iterative process reflects what Lee Boonstra describes in her whitepaper: "prompt engineering is an iterative process. Inadequate prompts can lead to ambiguous, inaccurate responses, and can hinder the model's ability to provide meaningful output"[^2].

## Lessons Learned from Prompt Engineering for Kaggle

My experience using prompt engineering for this Kaggle competition yielded several valuable insights:

### Specificity Drives Quality

The more specific and detailed my prompts were, the better the results. This aligns with PromptHub's first best practice: "Be specific"[^7]. When I clearly articulated requirements, constraints, and desired outcomes, the AI generated more relevant and usable content.

For example, in my code base prompt, specifying that the solution should "solve quality assurance in code deployments via agentic AI" narrowed the focus and resulted in more targeted code generation.

### Context is Crucial

Providing adequate context significantly improved the quality of AI-generated content. By including links to the competition, describing the problem domain, and (in the case of the blog article) sharing the actual code, I gave the models the information they needed to generate relevant outputs.

This approach is supported by OpenAI's recommendation to "provide reference text" when crafting prompts[^9].

### Structured Requests Yield Structured Results

Breaking down complex requests into structured components—as I did with the video script prompt—resulted in more organised and comprehensive outputs. This technique is particularly valuable for generating content with multiple sections or requirements.

As noted in TechTarget's best practices, "Step-by-step instructions can ensure that the model handles each aspect of a request"[^11].

### Iteration is Essential

Perhaps the most important lesson was that prompt engineering is not a one-and-done process. It requires iteration, refinement, and sometimes complete reformulation of prompts to achieve the desired results.

This iterative approach is similar to what Carla Cotas described in her Kaggle competition experience: "I completed this Kaggle competition on a challenge I set myself, within 10 week solve a competition on Kaggle"[^3]. Like traditional software development, AI-assisted development benefits from an iterative cycle of testing and improvement.

## The Future of AI-Assisted Development in Competitions

My experience with CodeGuardian suggests that prompt engineering will play an increasingly important role in competitive programming and AI development challenges. As noted in the LMSYS Kaggle competition analysis, participants are already leveraging LLMs "beyond the usual prompting \& RAG techniques"[^1].

For future Kaggle competitions, I anticipate several trends:

1. **More Sophisticated Prompt Chains**: Developers will likely create complex chains of prompts that build upon each other, with each prompt in the chain refining or extending the output of previous prompts.
2. **Hybrid Human-AI Development**: The most successful approaches will likely combine AI-generated code with human expertise, leveraging the strengths of both.
3. **Model-Specific Prompt Optimisation**: As different LLMs have different strengths and response patterns, competitors will develop model-specific prompting strategies to maximise performance.
4. **Automated Prompt Optimisation**: We may see the emergence of tools that automatically refine prompts based on the quality of generated outputs, similar to what Artur GR3 described in his winning LLMZoomCamp solution: "the techniques I used, such as structured outputs, chain of thought reasoning, multithreading, and error handling with retry mechanisms, can elevate most LLM-based applications to the next level"[^8].

## Conclusion

My journey developing CodeGuardian for the Kaggle Gen AI Intensive Course Capstone demonstrates the power of effective prompt engineering in AI-assisted development. By crafting thoughtful, specific, and context-rich prompts for different aspects of my project—code, documentation, and promotion—I was able to leverage LLMs as collaborative partners in the development process.

The experience reinforced that prompt engineering is both an art and a science, requiring creativity, technical understanding, and iterative refinement. As AI capabilities continue to advance, mastering the skill of prompt engineering will become increasingly valuable for developers, particularly in competitive contexts like Kaggle.

For those looking to enhance their own prompt engineering skills, resources like Learn Prompting's comprehensive guide[^6], which has been cited by major companies and used by Fortune 500 organisations, provide valuable insights and techniques that can be applied to a wide range of AI development scenarios.

As we move forward in this AI-powered era of software development, the ability to effectively communicate with and guide AI systems through well-crafted prompts will be a distinguishing skill for developers, particularly in competitive environments where innovation and efficiency are paramount.



[^1]: https://www.linkedin.com/pulse/llm-taming-interesting-insights-from-lymsys-kaggle-kiran-srqcc

[^2]: https://www.leeboonstra.dev/writing/write-prompting-whitepaper/

[^3]: https://www.linkedin.com/pulse/my-first-kaggle-competition-llm-classification-finetuning-cotas-dzsaf

[^4]: https://github.com/dair-ai/Prompt-Engineering-Guide

[^5]: https://aws.amazon.com/what-is/prompt-engineering/

[^6]: https://learnprompting.org/docs/introduction

[^7]: https://www.prompthub.us/blog/10-best-practices-for-prompt-engineering-with-any-model

[^8]: https://github.com/ArturGR3/LLM-kaggle-competition

[^9]: https://platform.openai.com/docs/guides/prompt-engineering

[^10]: https://blog.big-picture.com/en/the-10-best-free-prompt-engineering-courses-resources-for-chatgpt-midjourney-co/

[^11]: https://www.techtarget.com/searchenterpriseai/tip/Prompt-engineering-tips-and-best-practices

[^12]: https://cloud.google.com/discover/what-is-prompt-engineering

[^13]: https://github.com/dair-ai/Prompt-Engineering-Guide

[^14]: https://www.kaggle.com/code/ankitsingh1299/building-llms-generative-ai-prompt-engineering

[^15]: https://www.kaggle.com/competitions/llm-detect-ai-generated-text

[^16]: https://github.com/youssefHosni/Prompt-Engineering-for-Instruction-Tuned-LLM

[^17]: https://www.kaggle.com/competitions/llm-prompt-recovery/discussion/494503

[^18]: https://www.kaggle.com/competitions/kaggle-llm-science-exam

[^19]: https://www.kaggle.com/code/youssef19/prompt-engineering-best-practices

[^20]: https://www.kaggle.com/code/juliasuzuki/day-1-llm-prompt-engineering

[^21]: https://www.kaggle.com/competitions/llm-classification-finetuning

[^22]: https://www.kaggle.com/code/nghihuynh/unleashing-gemma-s-power-by-prompt-engineering

[^23]: https://www.youtube.com/watch?v=u81-7JWAZOY

[^24]: https://www.kaggle.com/discussions/general/381324

[^25]: https://www.kaggle.com/general/487123

[^26]: https://www.kaggle.com/whitepaper-prompt-engineering

[^27]: https://www.kaggle.com/competitions/llm-prompt-recovery/discussion/494525

[^28]: https://www.kaggle.com/code/markishere/day-1-prompting

[^29]: https://www.kaggle.com/datasets/jordanln/llm-prompts-in-the-context-of-machine-learning

[^30]: https://www.kaggle.com/code/chuaweicong/prompt-engineering-with-openai-api

[^31]: https://www.kaggle.com/competitions/llm-prompt-recovery/data

[^32]: https://www.kaggle.com/competitions/promptasaurus

[^33]: https://dev.to/get_pieces/10-prompt-engineering-best-practices-23dk

[^34]: https://www.spiceworks.com/tech/artificial-intelligence/articles/what-is-prompt-engineering/

[^35]: https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-the-openai-api

[^36]: https://www.promptingguide.ai/techniques

[^37]: https://www.reddit.com/r/PromptEngineering/comments/15464gs/best_prompt_engineering_resource/

[^38]: https://www.digitalocean.com/resources/articles/prompt-engineering-best-practices

[^39]: https://www.promptingguide.ai

[^40]: https://learnprompting.org

[^41]: https://www.promptingguide.ai/introduction/tips

[^42]: https://www.k2view.com/blog/prompt-engineering-techniques/

[^43]: https://developers.google.com/machine-learning/resources/prompt-eng

[^44]: https://www.reddit.com/r/LocalLLaMA/comments/1c5hxws/1000000_llm_competition_on_kaggle/

[^45]: https://www.youtube.com/watch?v=Kexbqd9ifM4

[^46]: https://www.reddit.com/r/PromptEngineering/comments/1ajz0tr/looking_for_platforms_hosting_prompt_engineering/

[^47]: https://www.lesswrong.com/posts/cZHezHezooJ4ryiro/benchmarking-llm-agents-on-kaggle-competitions

[^48]: https://www.youtube.com/watch?v=ddCYORu41Xs

[^49]: https://www.kaggle.com/code/peremartramanonellas/use-a-vectorial-db-to-optimize-prompts-for-llms

[^50]: https://www.youtube.com/watch?v=jijCxtqn2pA

[^51]: https://www.kaggle.com/code/utkarshsaxenadn/llms-prompt-engineering-dialog-summarization

[^52]: https://www.linkedin.com/pulse/excellent-resources-learn-ai-prompt-engineering-nasser-sami-bjdee