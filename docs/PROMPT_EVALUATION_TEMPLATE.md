# Prompt Evaluation Template

Use this template to systematically test and evaluate your prompts before deployment.

## Test Setup

### Prompt Information
- **Prompt Name**: _________________________
- **Version**: _________________________
- **Date**: _________________________
- **Model**: _________________________ (e.g., GPT-4, Claude-3.5, Gemini-1.5-Pro)
- **Tester**: _________________________

### Success Criteria
Define what "success" means for this prompt:

```markdown
Primary Metric: _________________________
Target Value: _________________________

Secondary Metrics:
- _________________________ (Target: _____)
- _________________________ (Target: _____)
- _________________________ (Target: _____)
```

---

## Test Case Template

Copy this section for each test case:

### Test Case #___

**Input:**
```
[Paste exact input here]
```

**Expected Output:**
```
[Describe what the ideal output should contain]
```

**Actual Output:**
```
[Paste actual model output here]
```

**Evaluation:**
- ✅ Pass / ❌ Fail / ⚠️ Partial
- **Accuracy**: ___/5 (1=incorrect, 5=perfect)
- **Format Compliance**: ___/5
- **Completeness**: ___/5
- **Clarity**: ___/5

**Issues Found:**
- [ ] Issue 1: _________________________
- [ ] Issue 2: _________________________

**Notes:**
_________________________

---

## Comprehensive Test Suite

### Category 1: Typical Use Cases (60% of tests)

Test the most common, expected inputs:

#### Test 1.1 - Standard Input
- **Input**: _________________________
- **Expected**: _________________________
- **Result**: ⬜ Pass ⬜ Fail
- **Notes**: _________________________

#### Test 1.2 - Standard Input (Variation)
- **Input**: _________________________
- **Expected**: _________________________
- **Result**: ⬜ Pass ⬜ Fail
- **Notes**: _________________________

[Continue for 10-15 typical cases]

### Category 2: Edge Cases (30% of tests)

Test boundary conditions and unusual inputs:

#### Test 2.1 - Minimum Input
- **Input**: _________________________
- **Expected**: _________________________
- **Result**: ⬜ Pass ⬜ Fail
- **Notes**: _________________________

#### Test 2.2 - Maximum Input
- **Input**: _________________________
- **Expected**: _________________________
- **Result**: ⬜ Pass ⬜ Fail
- **Notes**: _________________________

#### Test 2.3 - Ambiguous Input
- **Input**: _________________________
- **Expected**: _________________________
- **Result**: ⬜ Pass ⬜ Fail
- **Notes**: _________________________

#### Test 2.4 - Missing Information
- **Input**: _________________________
- **Expected**: _________________________
- **Result**: ⬜ Pass ⬜ Fail
- **Notes**: _________________________

[Continue for 5-10 edge cases]

### Category 3: Error Scenarios (10% of tests)

Test how prompt handles errors and invalid inputs:

#### Test 3.1 - Invalid Format
- **Input**: _________________________
- **Expected**: _________________________
- **Result**: ⬜ Pass ⬜ Fail
- **Notes**: _________________________

#### Test 3.2 - Contradictory Instructions
- **Input**: _________________________
- **Expected**: _________________________
- **Result**: ⬜ Pass ⬜ Fail
- **Notes**: _________________________

#### Test 3.3 - Out of Scope
- **Input**: _________________________
- **Expected**: _________________________
- **Result**: ⬜ Pass ⬜ Fail
- **Notes**: _________________________

[Continue for 3-5 error cases]

---

## Quantitative Metrics

### Accuracy Metrics

```markdown
Total Test Cases: _____
Passed: _____ (____%)
Failed: _____ (____%)
Partial: _____ (____%)

By Category:
- Typical Cases: _____% pass rate
- Edge Cases: _____% pass rate
- Error Cases: _____% pass rate
```

### Quality Scores (Average of all test cases)

```markdown
Accuracy: ___/5
Format Compliance: ___/5
Completeness: ___/5
Clarity: ___/5
Overall Quality: ___/5
```

### Performance Metrics

```markdown
Average Latency: _____ ms
Minimum Latency: _____ ms
Maximum Latency: _____ ms

Average Tokens Used: _____
Cost per Request: $_____
Total Test Cost: $_____
```

---

## Qualitative Analysis

### Strengths
What does this prompt do well?

1. _________________________
2. _________________________
3. _________________________

### Weaknesses
What issues were discovered?

1. _________________________
2. _________________________
3. _________________________

### Failure Pattern Analysis

#### Pattern 1: _________________________
- **Frequency**: _____/_____ test cases
- **Root Cause**: _________________________
- **Proposed Fix**: _________________________

#### Pattern 2: _________________________
- **Frequency**: _____/_____ test cases
- **Root Cause**: _________________________
- **Proposed Fix**: _________________________

---

## A/B Comparison (Optional)

### Variant A (Baseline)
- **Description**: _________________________
- **Pass Rate**: _____%
- **Avg Quality Score**: ___/5
- **Avg Latency**: _____ ms
- **Cost**: $_____

### Variant B (Test)
- **Description**: _________________________
- **Pass Rate**: _____%
- **Avg Quality Score**: ___/5
- **Avg Latency**: _____ ms
- **Cost**: $_____

### Statistical Significance
- **Sample Size**: _____ cases per variant
- **Improvement**: _____% (Variant B vs. A)
- **P-value**: _____
- **Significant?**: ⬜ Yes ⬜ No

### Recommendation
⬜ Use Variant A (baseline)
⬜ Use Variant B (test)
⬜ Continue testing
⬜ Try new approach

**Rationale**: _________________________

---

## Model Comparison (Optional)

Test the same prompt across different models:

| Model | Pass Rate | Quality | Latency | Cost | Notes |
|-------|-----------|---------|---------|------|-------|
| GPT-4 | ___% | ___/5 | ___ms | $___  | _____ |
| Claude-3.5 | ___% | ___/5 | ___ms | $___  | _____ |
| Gemini-1.5-Pro | ___% | ___/5 | ___ms | $___  | _____ |
| GPT-4o-mini | ___% | ___/5 | ___ms | $___  | _____ |

**Best Model for This Task**: _________________________
**Rationale**: _________________________

---

## Optimization Recommendations

### Priority 1 - Critical Issues
Issues that must be fixed before deployment:

1. **Issue**: _________________________
   - **Impact**: _________________________
   - **Fix**: _________________________
   - **Estimated Effort**: _________________________

2. **Issue**: _________________________
   - **Impact**: _________________________
   - **Fix**: _________________________
   - **Estimated Effort**: _________________________

### Priority 2 - Important Improvements
Issues that significantly impact quality:

1. **Issue**: _________________________
   - **Impact**: _________________________
   - **Fix**: _________________________
   - **Estimated Effort**: _________________________

### Priority 3 - Nice-to-Have
Minor improvements that enhance user experience:

1. **Issue**: _________________________
   - **Impact**: _________________________
   - **Fix**: _________________________
   - **Estimated Effort**: _________________________

---

## Deployment Readiness Checklist

### Functional Requirements
- [ ] Passes >90% of typical use cases
- [ ] Passes >70% of edge cases
- [ ] Handles errors gracefully
- [ ] Output format is consistent
- [ ] All constraints are respected

### Quality Standards
- [ ] Average quality score >4.0/5
- [ ] No critical failures in test suite
- [ ] Performance meets requirements
- [ ] Cost is within budget

### Documentation
- [ ] Prompt is version controlled
- [ ] Design decisions documented
- [ ] Test results recorded
- [ ] Usage guidelines created
- [ ] Known limitations listed

### Monitoring Plan
- [ ] Success metrics defined
- [ ] Logging implemented
- [ ] Error tracking configured
- [ ] Feedback collection mechanism ready
- [ ] Rollback plan documented

### Approval
⬜ **APPROVED** for production deployment
⬜ **APPROVED WITH CONDITIONS** (specify: ___________________)
⬜ **NOT APPROVED** - needs further work

**Approver**: _________________________
**Date**: _________________________
**Signature**: _________________________

---

## Post-Deployment Monitoring

### Week 1 Results
- **Total Requests**: _____
- **Success Rate**: _____%
- **Average Quality**: ___/5 (user ratings)
- **Incident Count**: _____
- **User Feedback**: _________________________

### Week 2 Results
- **Total Requests**: _____
- **Success Rate**: _____%
- **Average Quality**: ___/5
- **Incident Count**: _____
- **User Feedback**: _________________________

### Month 1 Summary
- **Total Requests**: _____
- **Success Rate**: _____%
- **Average Quality**: ___/5
- **Top Issues**: _________________________
- **Optimization Opportunities**: _________________________

### Action Items
1. [ ] _________________________
2. [ ] _________________________
3. [ ] _________________________

---

## Revision History

### Version 1.0
- **Date**: _________________________
- **Changes**: Initial version
- **Test Results**: ____% pass rate
- **Status**: _________________________

### Version 1.1
- **Date**: _________________________
- **Changes**: _________________________
- **Test Results**: ____% pass rate
- **Improvement**: +___% vs previous version
- **Status**: _________________________

[Add entry for each version]

---

## Appendix: Full Test Data

### Raw Test Results

```
Test ID | Input | Expected | Actual | Pass/Fail | Quality Score | Notes
--------|-------|----------|--------|-----------|---------------|-------
T1.1    | ...   | ...      | ...    | Pass      | 5/5           | ...
T1.2    | ...   | ...      | ...    | Fail      | 2/5           | ...
[Continue for all tests]
```

### Latency Distribution

```
Percentile | Latency (ms)
-----------|-------------
p50        | _____
p75        | _____
p90        | _____
p95        | _____
p99        | _____
```

### Token Usage Analysis

```
Metric                | Value
----------------------|-------
Avg Input Tokens      | _____
Avg Output Tokens     | _____
Avg Total Tokens      | _____
Max Tokens Observed   | _____
```

---

## Notes and Observations

### Testing Environment
- **Date Range**: _________________________
- **Testing Conditions**: _________________________
- **Known Variables**: _________________________

### Unexpected Behaviors
1. _________________________
2. _________________________
3. _________________________

### Ideas for Future Versions
1. _________________________
2. _________________________
3. _________________________

### Lessons Learned
1. _________________________
2. _________________________
3. _________________________
