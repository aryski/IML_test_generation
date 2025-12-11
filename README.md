# IML Test Generation Notebook

This notebook provides a framework for generating, evaluating, and selecting high-quality multiple-choice questions from text excerpts using large language models.

## Overview

The primary goal is to automate the creation of educational assessments. The process involves two main stages: generating questions with several LLMs and then using the same models to cross-evaluate the generated content based on a detailed rubric.

## Workflow

1.  **Question Generation**:
    *   Input text excerpts are loaded from `excerpts.xlsx`.
    *   Multiple LLMs generate questions based on a detailed prompt that specifies format, constraints, and desired cognitive diversity (referencing Bloom's Taxonomy).
    *   Generated questions are saved to individual CSV files per model.

2.  **Question Evaluation**:
    *   Each generated question is evaluated by all participating models against a six-point rubric.
    *   This cross-evaluation helps mitigate individual model bias and provides a more robust quality score.
    *   The evaluation metrics are:
        1.  **Cognitive Level**: Bloom's Taxonomy (1-5).
        2.  **Relevance**: How well the question is answered by the excerpt (1-5).
        3.  **Difficulty**: Overall challenge (1-5).
        4.  **Dependency**: Number of knowledge domains required (1-5).
        5.  **Ambiguousness**: Clarity of wording (1-5, lower is better).
        6.  **Context Dependency**: Portion of the excerpt needed to answer (1-5).

3.  **Analysis & Selection**:
    *   The notebook aggregates evaluation scores and provides radar charts to visualize and compare model performance, both as question generators and as evaluators.
    *   A final `select_top_questions` function ranks questions based on a weighted scoring mechanism, allowing a user to curate a final set of questions based on desired difficulty levels and quality metrics.

## Models Used

The following models are utilized for both generation and evaluation:

*   `o4-mini`
*   `o3`
*   `grok-3-beta`
*   `claude-3-7-sonnet-20250219`

## How to Use

1.  **Setup**:
    *   Install dependencies: `pip install -q openai pandas openpyxl seaborn`
    *   Add API keys for OpenAI, X.AI, and Anthropic in the "Secrets" section.
2.  **Input**:
    *   Place your source material in the `excerpts.xlsx` file, with one text excerpt per row in a column named `excerpt`.
3.  **Execution**:
    *   Run the notebook cells sequentially to generate, evaluate, and analyze the questions.
4.  **Customization**:
    *   Modify the `difficulty_levels` list in the final section to control the difficulty mix of the selected questions for your assessment.
    *   The scoring logic within `select_top_questions` can be adjusted to prioritize different metrics.

---

**Attribution**: The data and ideas for this project originate from the course material of PhD Anna Wróblewska, developed for the "Wstęp do uczenia maszynowego" class at MiNI.