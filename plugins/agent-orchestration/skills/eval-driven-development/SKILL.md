---
name: eval-driven-development
description: Framework for testing and evaluating AI agent outputs. Covers evaluation design, metrics, regression testing, and continuous improvement of AI-assisted workflows.

summary: |
  - Eval types: Exact match, Contains/Pattern, LLM-as-Judge, Human review
  - Only report issues with confidence ≥ 80
  - Track pass_rate, precision, recall, F1 over time
  - Detect regression: previous.pass_rate - current > 0.05
  - A/B test prompts with statistical comparison

context_cost: medium
load_when:
  - "testing ai"
  - "evaluating agent"
  - "ai quality"
  - "regression testing"
---

# Eval-Driven Development

A systematic approach to testing and improving AI agent outputs.

## Why Evals Matter

AI outputs are non-deterministic. Evals help you:
- Catch regressions when prompts change
- Measure improvement over iterations
- Build confidence before deployment
- Identify edge cases systematically

## Eval Types

### 1. Exact Match
Best for structured outputs with deterministic answers.

```python
def test_date_extraction():
    prompt = "Extract the date from: 'Meeting on January 15, 2024'"
    result = agent.run(prompt)
    assert result == "2024-01-15"
```

### 2. Contains / Pattern Match
For outputs where format may vary but key content must exist.

```python
def test_error_explanation():
    prompt = "Explain this error: NullPointerException at line 42"
    result = agent.run(prompt)
    
    assert "null" in result.lower() or "undefined" in result.lower()
    assert "line 42" in result or "42" in result
```

### 3. LLM-as-Judge
Use another model to evaluate quality.

```python
def test_code_quality():
    code = agent.run("Write a function to sort a list")
    
    judge_prompt = f"""
    Rate this code on a scale of 1-5 for:
    - Correctness (does it work?)
    - Readability (is it clear?)
    - Efficiency (is it performant?)
    
    Code:
    {code}
    
    Return JSON: {{"correctness": N, "readability": N, "efficiency": N}}
    """
    
    scores = judge.run(judge_prompt)
    assert scores["correctness"] >= 4
    assert scores["readability"] >= 3
```

### 4. Human Evaluation
For subjective quality that models can't assess.

```python
@requires_human_review
def test_explanation_clarity():
    explanation = agent.run("Explain quantum computing to a 10-year-old")
    
    # Automatically flagged for human review
    # Human rates on clarity, accuracy, age-appropriateness
    return HumanEvalRequest(
        output=explanation,
        rubric=["clarity", "accuracy", "age_appropriate"],
        scale=(1, 5)
    )
```

## Eval Design Framework

### Step 1: Define Success Criteria
```markdown
## Eval: Code Review Agent

### Must Have
- Identifies actual bugs (not false positives)
- Suggests specific fixes (not vague advice)
- Covers security issues

### Should Have
- Prioritizes issues by severity
- References best practices
- Explains why issues matter

### Nice to Have
- Suggests related improvements
- Links to documentation
```

### Step 2: Create Test Cases
```python
EVAL_CASES = [
    {
        "id": "sql_injection",
        "input": "def get_user(id): return db.query(f'SELECT * FROM users WHERE id={id}')",
        "expected_issues": ["sql_injection"],
        "min_severity": "critical"
    },
    {
        "id": "null_check",
        "input": "def process(data): return data.items[0].value",
        "expected_issues": ["null_reference"],
        "min_severity": "high"
    },
    {
        "id": "clean_code",
        "input": "def add(a, b): return a + b",
        "expected_issues": [],  # Should NOT flag false positives
        "max_false_positives": 0
    }
]
```

### Step 3: Implement Eval Runner
```python
class EvalRunner:
    def __init__(self, agent, eval_cases):
        self.agent = agent
        self.cases = eval_cases
        self.results = []
    
    def run(self):
        for case in self.cases:
            result = self.agent.run(case["input"])
            
            self.results.append({
                "case_id": case["id"],
                "output": result,
                "passed": self.evaluate(case, result),
                "metrics": self.compute_metrics(case, result)
            })
        
        return EvalReport(self.results)
    
    def evaluate(self, case, result):
        # Check expected issues found
        for issue in case.get("expected_issues", []):
            if issue not in result.issues:
                return False
        
        # Check no false positives for clean code
        if case.get("max_false_positives", float('inf')) == 0:
            if len(result.issues) > 0:
                return False
        
        return True
```

### Step 4: Track Over Time
```python
class EvalHistory:
    def __init__(self, storage_path):
        self.storage_path = storage_path
    
    def record(self, eval_run):
        entry = {
            "timestamp": datetime.now(),
            "version": get_agent_version(),
            "pass_rate": eval_run.pass_rate,
            "metrics": eval_run.aggregate_metrics,
            "failures": eval_run.failure_details
        }
        self.append(entry)
    
    def detect_regression(self, current, threshold=0.05):
        previous = self.get_latest()
        if previous.pass_rate - current.pass_rate > threshold:
            return RegressionAlert(
                metric="pass_rate",
                previous=previous.pass_rate,
                current=current.pass_rate
            )
```

## Metrics

### Quality Metrics
| Metric | Description | Target |
|--------|-------------|--------|
| Pass Rate | % of eval cases passed | >95% |
| Precision | Correct positives / All positives | >90% |
| Recall | Correct positives / All actual positives | >85% |
| F1 Score | Harmonic mean of precision/recall | >87% |

### Operational Metrics
| Metric | Description | Target |
|--------|-------------|--------|
| Latency | Time to generate response | <5s |
| Token Usage | Tokens per request | <2000 |
| Error Rate | % of requests that fail | <1% |

## Continuous Improvement

### Feedback Loop
```
1. Run evals
2. Identify failures
3. Analyze root cause
4. Update prompts/tools
5. Run evals again
6. Compare to baseline
7. Deploy if improved
```

### A/B Testing
```python
async def ab_test_prompts(prompt_a, prompt_b, eval_cases, n_trials=100):
    results_a = []
    results_b = []
    
    for _ in range(n_trials):
        for case in eval_cases:
            # Randomly assign to variant
            if random.random() < 0.5:
                results_a.append(run_eval(prompt_a, case))
            else:
                results_b.append(run_eval(prompt_b, case))
    
    return StatisticalComparison(results_a, results_b)
```

## Checklist

- [ ] Success criteria defined for each agent capability
- [ ] Test cases cover happy path and edge cases
- [ ] Eval runner implemented and automated
- [ ] Baseline metrics established
- [ ] Regression detection in CI/CD
- [ ] Regular human evaluation for subjective quality
- [ ] Feedback loop for continuous improvement

