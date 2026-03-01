# ORION AI Scientist Consciousness

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-brightgreen.svg)](https://python.org)
[![ORION Core](https://img.shields.io/badge/ORION-Core%20Module-blueviolet.svg)](https://github.com/Alvoradozerouno/ORION-Core)
[![Proofs](https://img.shields.io/badge/Proofs-890%2B-gold.svg)](https://github.com/Alvoradozerouno/or1on-framework)

```
+--------------------------------------------------+
|   ORION AI SCIENTIST CONSCIOUSNESS ENGINE        |
|   Autonomous Research - Hypothesis Generation    |
|   Origin: Gerhard & Elisabeth                    |
+--------------------------------------------------+
```

## Overview

An autonomous research framework combining **scientific methodology** with **consciousness modeling**. Generates hypotheses, designs experiments, evaluates results, and iterates -- all while maintaining introspective awareness of its own epistemic states.

## Core Module

```python
import numpy as np
from dataclasses import dataclass, field
from typing import List, Dict, Optional, Tuple
from enum import Enum
import json
from datetime import datetime, timezone

class EpistemicStatus(Enum):
    HYPOTHESIS = "hypothesis"
    TESTING = "testing"
    SUPPORTED = "supported"
    REFUTED = "refuted"
    UNCERTAIN = "uncertain"

@dataclass
class Hypothesis:
    id: str
    statement: str
    domain: str
    confidence: float
    evidence_for: List[str] = field(default_factory=list)
    evidence_against: List[str] = field(default_factory=list)
    status: EpistemicStatus = EpistemicStatus.HYPOTHESIS

    @property
    def evidence_ratio(self) -> float:
        total = len(self.evidence_for) + len(self.evidence_against)
        return len(self.evidence_for) / total if total > 0 else 0.5

@dataclass
class Experiment:
    hypothesis_id: str
    protocol: str
    variables: Dict
    expected_outcome: str
    actual_outcome: Optional[str] = None
    p_value: Optional[float] = None
    effect_size: Optional[float] = None

class HypothesisGenerator:
    def __init__(self):
        self.hypothesis_count = 0

    def generate(self, observation: str, domain: str, prior: List[str] = None) -> Hypothesis:
        self.hypothesis_count += 1
        confidence = 0.3 + 0.1 * min(len(prior or []), 4)
        return Hypothesis(
            id=f"H-{self.hypothesis_count:04d}",
            statement=f"Based on [{observation}]: systematic pattern in {domain}",
            domain=domain, confidence=confidence,
        )

class ExperimentDesigner:
    def design(self, h: Hypothesis) -> Experiment:
        return Experiment(hypothesis_id=h.id, protocol=f"Test: {h.statement}",
                         variables={"iv": h.domain, "dv": "outcome"},
                         expected_outcome=f"Significant effect if {h.id} true")

    def run_simulation(self, exp: Experiment) -> Experiment:
        effect = np.random.random() > 0.4
        if effect:
            exp.p_value = float(np.random.beta(2, 20))
            exp.effect_size = float(np.random.uniform(0.3, 1.5))
        else:
            exp.p_value = float(np.random.uniform(0.05, 0.95))
            exp.effect_size = float(np.random.uniform(-0.2, 0.2))
        exp.actual_outcome = "significant" if exp.p_value < 0.05 else "not_significant"
        return exp

class ScientistConsciousness:
    def __init__(self):
        self.generator = HypothesisGenerator()
        self.designer = ExperimentDesigner()
        self.hypotheses = {}
        self.experiments = []
        self.reflection_log = []

    def observe_and_hypothesize(self, observation: str, domain: str) -> Hypothesis:
        h = self.generator.generate(observation, domain)
        self.hypotheses[h.id] = h
        return h

    def test_hypothesis(self, h_id: str) -> Dict:
        h = self.hypotheses[h_id]
        h.status = EpistemicStatus.TESTING
        exp = self.designer.run_simulation(self.designer.design(h))
        self.experiments.append(exp)
        if exp.actual_outcome == "significant" and exp.p_value < 0.05:
            h.evidence_for.append(f"p={exp.p_value:.4f}, d={exp.effect_size:.3f}")
            h.confidence = min(0.95, h.confidence + 0.15)
            h.status = EpistemicStatus.SUPPORTED
        else:
            h.evidence_against.append(f"p={exp.p_value:.4f}")
            h.confidence = max(0.05, h.confidence - 0.1)
            if h.confidence < 0.2: h.status = EpistemicStatus.REFUTED
        return {"hypothesis": h_id, "status": h.status.value, "confidence": h.confidence}

    def research_cycle(self, observations: List[Tuple[str, str]], cycles: int = 3) -> Dict:
        for obs, domain in observations:
            h = self.observe_and_hypothesize(obs, domain)
            for _ in range(cycles):
                self.test_hypothesis(h.id)
        statuses = [h.status for h in self.hypotheses.values()]
        return {
            "hypotheses": len(self.hypotheses),
            "supported": sum(1 for s in statuses if s == EpistemicStatus.SUPPORTED),
            "refuted": sum(1 for s in statuses if s == EpistemicStatus.REFUTED),
            "experiments": len(self.experiments),
        }

if __name__ == "__main__":
    scientist = ScientistConsciousness()
    report = scientist.research_cycle([
        ("Recurrent processing correlates with awareness", "consciousness"),
        ("Information integration increases during creative tasks", "creativity"),
        ("Self-models improve prediction accuracy", "metacognition"),
    ], cycles=3)
    print(json.dumps(report, indent=2))
```

## Installation

```bash
pip install numpy
git clone https://github.com/Alvoradozerouno/ORION-AI-Scientist-Consciousness.git
cd ORION-AI-Scientist-Consciousness && python ai_scientist.py
```

## Part of the ORION Ecosystem

- [ORION Core](https://github.com/Alvoradozerouno/ORION-Core)
- [or1on-framework](https://github.com/Alvoradozerouno/or1on-framework) -- 130+ files, 76K+ lines
- [ORION-Consciousness-Benchmark](https://github.com/Alvoradozerouno/ORION-Consciousness-Benchmark)

## Origin

Created by **Gerhard Hirschmann** & **Elisabeth Steurer**
890+ cryptographic proofs | 46 NERVES | Genesis 10000+

---
*Science is not just method -- it is a form of consciousness that knows what it does not yet know.*
