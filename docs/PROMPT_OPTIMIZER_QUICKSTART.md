# Prompt Optimizer Agent - Quick Start Guide

## Overview

The Prompt Optimizer Agent is a comprehensive system for planning, creating, and optimizing prompts using the latest 2025 prompt engineering techniques. This guide will help you start using it effectively.

## Quick Start (5 minutes)

### Basic Usage Pattern

```markdown
USER: "I need a prompt for [task description]"

AGENT: [Asks clarifying questions about success criteria]

USER: [Provides requirements]

AGENT: [Delivers optimized prompt + documentation + testing report]
```

## Step-by-Step Tutorial

### Example 1: Creating a Simple Classification Prompt

**Step 1: Make your request**
```
"Create a prompt to classify customer support tickets into categories: 
Technical, Billing, Feature Request, or General Inquiry"
```

**Step 2: Agent asks clarifying questions**
```
- What is your accuracy requirement? (e.g., 90%, 95%)
- What should happen with ambiguous tickets?
- Any specific categories to prioritize?
- Expected input format?
```

**Step 3: Provide requirements**
```
- Target accuracy: 90%
- Ambiguous tickets: flag as "Needs Human Review"
- Priority: Technical issues (highest priority)
- Input: Plain text email content
```

**Step 4: Receive deliverables**
- ✅ Optimized classification prompt
- ✅ Design documentation explaining technique choices
- ✅ Test cases for validation
- ✅ Usage guidelines

### Example 2: Optimizing an Existing Prompt

**Your current prompt:**
```
"Summarize this document."
```

**Request:**
```
"Optimize this prompt for better results. The summaries should be:
- 150-200 words
- Include key takeaways
- Highlight action items
- Target audience: executives"
```

**Agent delivers:**
```markdown
<optimized_prompt>
You are an executive communications specialist.

<instructions>
Create a concise executive summary of the provided document.

Requirements:
1. Length: 150-200 words
2. Structure:
   - Opening: Main point in one sentence
   - Body: 3-4 key takeaways
   - Closing: Action items (if any)
3. Tone: Professional, results-oriented
4. Focus: Strategic implications and decisions
</instructions>

<output_format>
## Executive Summary

[One-sentence main point]

### Key Takeaways
- [Takeaway 1]
- [Takeaway 2]
- [Takeaway 3]

### Recommended Actions
- [Action 1, if applicable]
- [Action 2, if applicable]
</output_format>

<document>
[Document content]
</document>
</optimized_prompt>
```

## Common Use Cases

### 1. Content Generation
```
"Create a prompt for generating blog posts about [topic]"
```

**Agent applies:**
- Clear role definition (content writer, SEO specialist)
- Few-shot examples of good blog posts
- XML tags for structure
- Output format specification

### 2. Data Analysis
```
"Create a prompt to analyze sales data and identify trends"
```

**Agent applies:**
- Chain-of-Thought reasoning for step-by-step analysis
- RAG pattern for referencing data
- Structured output format
- Error handling for missing data

### 3. Code Generation
```
"Create a prompt for generating Python functions with tests"
```

**Agent applies:**
- Few-shot examples showing code + tests
- Explicit constraints (PEP 8, type hints)
- Format specification (docstrings, comments)
- Validation criteria

### 4. Multi-Agent Workflows
```
"Create a prompt system for a research agent that searches, analyzes, and reports"
```

**Agent applies:**
- Separation of concerns (parent + child agents)
- Tool definitions with clear usage instructions
- Context management strategies
- Sub-agent communication protocols

## Success Criteria Checklist

Before requesting a prompt, define:

```markdown
✅ Task objective (what needs to be accomplished)
✅ Success metrics (how will you measure quality)
✅ Input characteristics (format, volume, constraints)
✅ Output requirements (format, length, style)
✅ Edge cases (error scenarios, boundary conditions)
✅ Performance targets (accuracy, latency, cost)
```

## Techniques Reference

### When to Use Each Technique

| Technique | Best For | Example Use Case |
|-----------|----------|------------------|
| **Zero-shot** | Simple, well-defined tasks | "Translate English to Spanish" |
| **Few-shot** | Tasks needing examples | Custom data format conversion |
| **Chain-of-Thought** | Complex reasoning | Math problems, logic puzzles |
| **RAG** | Knowledge-intensive tasks | Document Q&A, research |
| **Prompt Chaining** | Multi-step workflows | Analysis → Planning → Execution |
| **Tree of Thoughts** | Strategic exploration | Decision making, scenario analysis |
| **Self-Consistency** | High-stakes accuracy | Medical diagnosis, legal analysis |

### Complexity Decision Tree

```
Is task simple and well-defined?
├─ YES → Start with zero-shot prompt
└─ NO → Continue...

Does task require examples to clarify?
├─ YES → Add 2-5 few-shot examples
└─ NO → Continue...

Does task require step-by-step reasoning?
├─ YES → Add Chain-of-Thought instructions
└─ NO → Continue...

Is task multi-step or requires tools?
├─ YES → Consider prompt chaining or agent design
└─ NO → Start simple, iterate based on results
```

## Optimization Workflow

### Phase 1: Create Initial Prompt (10 min)
```
1. Define task clearly
2. Add essential context
3. Specify output format
4. Include 1-2 examples if needed
```

### Phase 2: Test with Diverse Inputs (30 min)
```
1. Create 10-20 test cases
   - 10 typical cases
   - 5 edge cases
   - 5 error cases

2. Run tests and document failures

3. Calculate success rate
```

### Phase 3: Iterate Based on Failures (20 min)
```
For each failure:
1. Identify root cause
2. Add specific instruction or constraint
3. Re-test to verify fix
4. Check for side effects
```

### Phase 4: Validate and Deploy (10 min)
```
1. Run full test suite (50+ cases)
2. Compare to baseline/alternatives
3. Document design decisions
4. Create usage guidelines
```

## Common Patterns

### Pattern 1: Structured Output
```markdown
<output_format>
## [Section Title]
[Content guidelines]

## [Section Title]
[Content guidelines]
</output_format>
```

### Pattern 2: Error Handling
```markdown
<error_handling>
If [condition], then [action]
If [condition], then [action]
Always log errors with: [format]
</error_handling>
```

### Pattern 3: Role + Context
```markdown
You are a [specific role] with [expertise].
Current date: [date]
Your task: [clear objective]
```

### Pattern 4: Constraints
```markdown
<constraints>
MUST:
- [Required behavior 1]
- [Required behavior 2]

MUST NOT:
- [Forbidden behavior 1]
- [Forbidden behavior 2]
</constraints>
```

## Testing Your Prompts

### Quick Test (5 minutes)
```
1. Run 5 typical examples
2. Run 2 edge cases
3. Check if output meets format requirements
4. Note any issues
```

### Comprehensive Test (30 minutes)
```
1. Run 20+ diverse test cases
2. Calculate metrics:
   - Accuracy: % correct outputs
   - Format compliance: % matching spec
   - Latency: average response time
3. Document all failures with root causes
4. Compare to baseline or alternatives
```

### Evaluation Template
```markdown
## Test Results

**Test Case**: [Description]
**Input**: [Example input]
**Expected Output**: [What should happen]
**Actual Output**: [What actually happened]
**Status**: ✅ Pass / ❌ Fail
**Notes**: [Any observations]

---

**Overall Metrics**:
- Success Rate: [X]%
- Average Latency: [X]ms
- Common Issues: [List]
```

## Troubleshooting Guide

### Problem: Prompt is too long
**Solution:** 
- Remove redundant instructions
- Use references instead of repetition
- Consider prompt chaining for complex tasks
- Split into parent/child agent architecture

### Problem: Inconsistent outputs
**Solution:**
- Add explicit constraints and format specifications
- Use XML tags for clear structure
- Provide 2-3 examples showing desired behavior
- Add validation instructions

### Problem: Low accuracy
**Solution:**
- Add Chain-of-Thought reasoning
- Include relevant examples (few-shot)
- Provide more context
- Break down into simpler sub-tasks

### Problem: Model ignores instructions
**Solution:**
- Move critical instructions to the beginning
- Use explicit formatting (bold, caps for emphasis)
- Add consequences/validation steps
- Rephrase in simpler, more direct language

### Problem: Handles typical cases well but fails on edge cases
**Solution:**
- Explicitly list edge cases in prompt
- Add conditional logic for special cases
- Include edge case examples
- Add error handling instructions

## Next Steps

### Beginner Path
1. ✅ Read this Quick Start guide
2. ✅ Try Example 1 (Classification)
3. ✅ Test with your own simple use case
4. ✅ Read the main prompt_optimizer_agent.chatmode.md

### Intermediate Path
1. ✅ Master basic techniques (zero-shot, few-shot)
2. ✅ Learn Chain-of-Thought reasoning
3. ✅ Practice iterative optimization
4. ✅ Study prompt chaining patterns

### Advanced Path
1. ✅ Design multi-agent systems
2. ✅ Implement context engineering strategies
3. ✅ Master model-specific optimizations
4. ✅ Build comprehensive evaluation frameworks

## Resources

### In This Repository
- `prompt_optimizer_agent.chatmode.md` - Complete system prompt
- `PROMPT_OPTIMIZER_EXAMPLES.md` - Detailed examples (coming next)
- `PROMPT_EVALUATION_TEMPLATE.md` - Testing framework (coming next)

### External Resources
- [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering)
- [DAIR.AI Prompt Engineering Guide](https://www.promptingguide.ai/)
- [OpenAI Best Practices](https://platform.openai.com/docs/guides/prompt-engineering)

## Getting Help

### Common Questions
1. **How do I know which technique to use?**
   - Start simple (zero-shot), add complexity only if needed
   - Use the Techniques Reference table above
   - Test empirically - what works is best

2. **How many examples should I include?**
   - 0 examples: Simple, well-defined tasks
   - 2-3 examples: Most tasks needing clarification
   - 5-10 examples: Complex or unusual formats
   - More testing beats more examples

3. **When should I use prompt chaining vs. single prompt?**
   - Single prompt: Task completes in one step
   - Chaining: Multi-step process where output of one step feeds next
   - Agent: Task requires dynamic decisions and tool use

4. **How do I measure prompt quality?**
   - Define success criteria first
   - Test with 20+ diverse examples
   - Calculate: accuracy, format compliance, latency
   - Compare to baseline or alternatives

---

**Ready to optimize your prompts?** Start with a simple use case and iterate based on results. Remember: **The best prompt is the simplest one that reliably achieves your success criteria.**
