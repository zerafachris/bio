---
title: "How Airbnb Leveraged Large Language Models for a Groundbreaking Code Migration"
tags:
  - AI
  - LLM
toc: true
---

<figure>
	<a href=""><img src="https://i.imgur.com/6kQfQVo.jpeg"></a>
</figure>

Airbnb recently completed an ambitious and innovative project: migrating 3,500 React component test files from Enzyme to React Testing Library (RTL). This task, initially estimated to require 1.5 years of manual engineering effort, was accomplished in just six weeks. The secret? A combination of frontier large language models (LLMs) and a robust automation pipeline. This article explores the challenges Airbnb faced, the role LLMs played in overcoming them, and how the team structured its tools to achieve this feat at scale.

### **The Challenge: Moving from Enzyme to React Testing Library**

Enzyme, once a popular choice for testing React components, became increasingly misaligned with modern React practices. Airbnb began transitioning to React Testing Library in 2020 for new tests but still had thousands of legacy Enzyme tests that needed updating. A simple swap wasn’t feasible due to fundamental differences between the two frameworks. Deleting the old tests would have left significant gaps in code coverage.

Manually refactoring these tests was not only time-consuming but also error-prone. The challenge was clear: how could Airbnb automate this migration while preserving the intent and coverage of the original tests?

### **How Airbnb Solved It: LLM-Driven Automation**

#### **1. Hackathon Inspiration**

The idea of using LLMs for this migration was first explored during an internal hackathon in mid-2023. The team demonstrated that LLMs could convert hundreds of test files in just days. Encouraged by these results, Airbnb expanded this approach into a scalable migration pipeline.

#### **2. A Step-Based Automation Pipeline**

The migration process was structured as a state machine, where each test file moved through discrete validation and refactor steps:

- Refactoring from Enzyme to RTL
- Fixing Jest compatibility issues
- Addressing linting and TypeScript errors
- Marking files as complete after passing all checks

This modular approach allowed parallel processing of hundreds of files at once, enabling rapid progress.

#### **3. Retry Loops with Dynamic Prompting**

To handle migration failures, Airbnb implemented retry loops. If a file failed validation at any step, the system dynamically updated prompts with detailed error messages and retried up to a configurable limit. This brute-force strategy proved effective for simple-to-medium complexity files.

#### **4. Expanding Context for Complex Files**

For more intricate test setups, the team enriched LLM prompts with extensive context:

- Source code of the component under test
- Related test files from the same directory
- Examples of well-written RTL tests
- General migration guidelines

Prompts ranged from 40,000 to 100,000 tokens, enabling the LLM to understand team-specific patterns and codebase architecture.

#### **5. Iterative Refinement: "Sample, Tune, Sweep"**

After achieving a 75% success rate on their first bulk run, Airbnb tackled the remaining 25% using an iterative process:

1. Identify common issues in failing files.
2. Update prompts and scripts to address these issues.
3. Re-run migrations on failing files.
4. Repeat until reaching diminishing returns.

This systematic approach increased the success rate to 97%, leaving only 3% of files for manual intervention.

### **Results and Impact**

Airbnb’s LLM-driven migration yielded remarkable results:

- **Time Savings:** The entire migration was completed in six weeks instead of 1.5 years.
- **High Automation Success:** 97% of files were migrated automatically.
- **Cost Efficiency:** Even with high API usage and engineering time, the cost was significantly lower than manual migration.
- **Preserved Quality:** Original test intent and code coverage were maintained throughout the process.

### **Lessons Learned and Future Applications**

This project highlights how LLMs can excel at large-scale code transformations:

1. Breaking tasks into modular steps simplifies automation.
2. Dynamic retry loops improve success rates for moderately complex tasks.
3. Providing rich context enables LLMs to handle intricate scenarios effectively.
4. Iterative refinement ensures continuous improvement.

Airbnb plans to expand its use of LLM-powered automation for other engineering challenges, further enhancing developer productivity. Full details of this work is available on [Airbnb Tech Blog](https://medium.com/airbnb-engineering/accelerating-large-scale-test-migration-with-llms-9565c208023b)