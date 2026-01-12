# Framework to automatically rectify Web Accessibility Violations in the DOM.
![workflow](./1721070748538.jpeg)


# LLM-Based Web Accessibility Violation Repair

This repository contains the code for my Master's thesis research evaluating GPT-4 and Claude 3 as tools for automatically detecting and repairing web accessibility violations in real-time.

## Research Overview

**Problem:** Over 82% of websites (1.6B+) have accessibility violations, making the web unusable for people with disabilities. Manual remediation at scale is impractical.

**Approach:** Built an automated pipeline that:
1. Crawls target URLs and runs accessibility audits using Puppeteer + axe-core
2. Extracts violating HTML elements from the DOM
3. Sends violations to GPT-4 and Claude 3 with structured prompts
4. Swaps corrected HTML back into the DOM
5. Re-runs accessibility tests to verify fixes

**Prompt Engineering Experiments:** Compared three techniques across varying temperature settings:
- Few-shot prompting
- Chain-of-thought prompting  
- ReAct prompting (thought → reasoning → action loops)

## Results

| Model | Violations Tested | Fix Rate |
|-------|------------------|----------|
| GPT-4 | 776 | 86.7% |
| Claude 3 | 641 | 78.0% |

**Key Finding:** ReAct prompting significantly outperformed other techniques for complex violations (e.g., color contrast) by enabling iterative self-correction. For color contrast specifically, ReAct prompts incorporated WCAG ratio calculations and brand color preservation constraints, allowing models to verify and regenerate solutions until meeting accessibility thresholds.

## Violation Types Tested

- Color contrast (WCAG AA/AAA compliance)
- Missing alt text on images
- Non-descriptive link text
- Form label associations
- ARIA attribute violations

## Project Structure
```
├── app.js              # Entry point
├── LLM/                # GPT-4 and Claude 3 API integration + prompt templates
├── Operations/         # DOM manipulation and HTML swapping
├── RunAccessibilityTest/  # Puppeteer + axe-core test runner
└── Files/              # Output reports (before/after analysis)
```

## Setup
```bash
npm install
node app.js  # Provide target URLs in config
```

## Output

Each analysis generates three files:
- Accessibility report before repair
- Accessibility report after repair  
- Detailed analysis results with per-violation outcomes

## Technologies

Node.js, Puppeteer, axe-core, OpenAI API, Anthropic API

## Author

Mide Ibraheem — MSc Computer Science, Northumbria University (2024)
