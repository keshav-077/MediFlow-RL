<div align="center">

```
███╗   ███╗███████╗██████╗ ██╗███████╗██╗      ██████╗ ██╗    ██╗
████╗ ████║██╔════╝██╔══██╗██║██╔════╝██║     ██╔═══██╗██║    ██║
██╔████╔██║█████╗  ██║  ██║██║█████╗  ██║     ██║   ██║██║ █╗ ██║
██║╚██╔╝██║██╔══╝  ██║  ██║██║██╔══╝  ██║     ██║   ██║██║███╗██║
██║ ╚═╝ ██║███████╗██████╔╝██║██║     ███████╗╚██████╔╝╚███╔███╔╝
╚═╝     ╚═╝╚══════╝╚═════╝ ╚═╝╚═╝     ╚══════╝ ╚═════╝  ╚══╝╚══╝ 
```

# 🏥 **MediFlow-RL**

### *Advanced Reinforcement Learning for Pharmaceutical Supply Chain Optimization*

**Developed by Keshav**

---

[![OpenEnv](https://img.shields.io/badge/OpenEnv-Compatible-00C7B7?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjAiIGhlaWdodD0iMjAiIHZpZXdCb3g9IjAgMCAyMCAyMCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48Y2lyY2xlIGN4PSIxMCIgY3k9IjEwIiByPSI5IiBzdHJva2U9IndoaXRlIiBzdHJva2Utd2lkdGg9IjIiLz48L3N2Zz4=)](https://huggingface.co/spaces/keshav/MediFlow-RL)
[![Live Demo](https://img.shields.io/badge/🤗_Live-Demo-FFD21E?style=for-the-badge)](https://huggingface.co/spaces/keshav/MediFlow-RL)
[![Gymnasium](https://img.shields.io/badge/Gymnasium-0.29+-8B5CF6?style=for-the-badge&logo=gymnasium)](https://gymnasium.farama.org)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-22C55E?style=for-the-badge)](LICENSE)

</div>

---

## 🌍 **The Global Crisis**

> ### **WHO estimates 25–50% of vaccines worldwide are wasted due to cold chain failures.**

Every year, millions of dollars in life-saving pharmaceuticals are destroyed—not from manufacturing defects, but from **preventable logistics failures**:

- 🚨 Choosing routes without considering refrigeration degradation
- ⚠️ Missing critical depot stops during temperature emergencies
- ❌ Failing to prioritize organ shipments over routine deliveries
- 💔 Preventable deaths in low-resource healthcare settings

**A single wrong decision can destroy an entire medical shipment.**

---

## 💡 **The Solution: MediFlow-RL**

**MediFlow-RL** is the world's first **open-source reinforcement learning environment** that models the **complete complexity** of pharmaceutical cold chain logistics:

✅ **Dual-objective optimization** (time + temperature)  
✅ **Stochastic refrigeration failure** (Working → Degraded → Failed)  
✅ **Multi-priority cargo triage** (Organs, Blood, Vaccines, Insulin)  
✅ **Cold depot diversion mechanics** with real-time cost calculation  
✅ **Cascading failure scenarios** (heatwave + breakdown + deadline pressure)  
✅ **GRPO-compatible graders** for group-relative policy optimization  

This isn't just another logistics simulator—**it's a training ground for AI that could save lives.**

---

## 🎯 **What Makes This Unique?**

<div align="center">

| Feature | MediFlow-RL | Standard Logistics Envs |
|---------|-------------|-------------------------|
| 🌡️ **Temperature Physics** | Newton's Law of Cooling per cargo type | ❌ Not modeled |
| ❄️ **Refrigeration Failure** | 3-state stochastic degradation | ❌ Not modeled |
| 🏥 **Cold Depot Diversion** | Explicit action with detour cost | ❌ Not modeled |
| 🩺 **Medical Cargo Triage** | Organs, blood, vaccines, insulin | ❌ Not modeled |
| ⚡ **Cascading Failures** | Multi-condition stress scenarios | ❌ Not modeled |
| 🎓 **GRPO Graders** | 4-tier scalar reward [0,1] | Rarely available |
| 🧪 **Adversarial Seeds** | Hardcoded stress tests (Hard/Extreme) | Rarely available |

</div>

---

## 🏗️ **Environment Architecture**

You are a **dispatch controller**—a command center managing a fleet of refrigerated vehicles across a city network. Every 15 simulated minutes (one step), you decide:

🚛 **Where should each vehicle route next?**  
❄️ **Should we divert to a cold depot for emergency cooling?**  
🔄 **Can we swap cargo between vehicles to recover from breakdowns?**  
⚡ **Should we expedite (burn fuel) to meet critical deadlines?**  
🛑 **Is this shipment unrecoverable—should we abort?**  

```
╔═══════════════════════════════════════════════════════════╗
║                     CITY GRAPH NETWORK                    ║
║                                                           ║
║    [HUB] ──3──● ──2──[❄️ COLD DEPOT]──4──●              ║
║      │             │                      │               ║
║      5             8                      2               ║
║      │             │                      │               ║
║      ● ──1──● ──6──[❄️ COLD DEPOT]    [🏥 HOSPITAL ★★★] ║
║             │                                             ║
║             3                                             ║
║             │                                             ║
║          [🏥 CLINIC ★]                                    ║
║                                                           ║
║   ★ = delivery destination                                ║
║   numbers = travel time (steps, traffic-adjusted)         ║
╚═══════════════════════════════════════════════════════════╝
```

---

## 🧬 **Medical Cargo Types & Thermal Constraints**

<div align="center">

| Cargo | Icon | Safe Range | Excursion Tolerance | Zero-Tolerance? |
|-------|------|------------|---------------------|-----------------|
| **Vaccine** | 💉 | 2°C – 8°C | 30 steps | No |
| **Insulin** | 🩸 | 2°C – 8°C | 20 steps | No |
| **Blood** | 🫀 | 1°C – 6°C | 10 steps | No |
| **Organ** | 🫁 | 0°C – 4°C | **0 steps** | **YES—instant failure** |

</div>

**Key Design Principle:** Organs have **zero thermal tolerance**. A single temperature excursion = complete shipment loss. This forces agents to learn **proactive decision-making**, not reactive patching.

---

## 🎮 **Agent Observation Space**

```python
observation = {
    "global": (7,)        # ambient_temp, traffic_level, weather_event,
                          # time_of_day, episode_progress
    
    "vehicles": (N, 9+M)  # location, status, refrigeration_state, fuel,
                          # nearest_cold_depot_id,
                          # detour_cost_to_depot ← CRITICAL SIGNAL
    
    "shipments": (M, 13)  # current_temp, temp_lower_bound, temp_upper_bound,
                          # excursion_steps, deadline_remaining, priority
}
```

### 🔑 **Key Innovation: `detour_cost_to_depot`**

At every step, the environment runs **Dijkstra's algorithm** to compute exactly how many extra steps a cold depot diversion would cost given current traffic conditions. 

**The agent never navigates the graph manually**—it only decides **whether** to divert. This design choice:
- ✅ Keeps action space tractable
- ✅ Focuses learning on decision-making, not pathfinding
- ✅ Mirrors real dispatch center operations

---

## ⚙️ **Action Space**

<div align="center">

| Action | Description | Use Case |
|--------|-------------|----------|
| `REROUTE` | Change next waypoint | Triage, deadline pressure |
| `DIVERT_COLD_DEPOT` | Emergency cooling | Refrigeration degrading |
| `SWAP_VEHICLE` | Transfer cargo | Breakdown recovery |
| `EXPEDITE` | Burn fuel for speed | Critical deadline |
| `ABORT` | Return to hub | Unrecoverable situation |
| `WAIT` | Hold position | Vehicle in transit |

</div>

All invalid actions are **automatically masked** (compatible with `MaskablePPO`).

---

## 🏆 **Four-Tier Evaluation System**

Every trained policy is evaluated deterministically across **four difficulty tiers**. All graders return scalar scores in **[0.0, 1.0]**.

```
┌─────────────┬────────────────────────────────────────────┬───────────┐
│ Tier        │ Scenario                                   │ Threshold │
├─────────────┼────────────────────────────────────────────┼───────────┤
│ 🟢 Easy     │ 1 vehicle · 1 vaccine · no weather         │   0.80    │
│ 🟡 Moderate │ 2 vehicles · 3 shipments · heatwaves       │   0.65    │
│ 🔴 Hard     │ 3 vehicles · 5 shipments · tight deadlines │   0.50    │
│ ⚫ Extreme   │ 5 vehicles · 8 shipments · organ priority  │   0.35    │
└─────────────┴────────────────────────────────────────────┴───────────┘
```

### 🎯 **Current Benchmark Performance**

*Evaluated at training step 50,000 · seed=42 · deterministic rollout*

```
🟢 Easy      ████████████████████████  0.9974  ✅ PASS
🟡 Moderate  █████████████████████░░░  0.8899  ✅ PASS
🔴 Hard      █████████████████░░░░░░░  0.7200  ✅ PASS
⚫ Extreme   ██████████████░░░░░░░░░░  0.5800  ✅ PASS

Overall Score: 0.7968
```

**Hard** and **Extreme** tiers inject **adversarial seeds**:
- 💥 Simultaneous breakdown + heatwave
- 🫁 Organ delivery during power outage
- ⏰ Clustered deadlines under traffic surge

Passing Extreme tier proves the agent learned **pharmaceutical triage logic**, not just routing optimization.

---

## 🧠 **Training Architecture**

MediFlow-RL uses a **3-phase curriculum** with `MaskablePPO`:

```
Phase 1 ──────▶ Phase 2 ──────▶ Phase 3
Easy/Moderate   Moderate/Hard   Hard/Extreme
     │               │                │
     └───────────────┴────────────────┘
          Fixed tensor shape throughout
       (safe checkpoint resumption)
```

**Key Training Innovations:**
- 🎯 **Fixed observation shape** across all difficulties (zero-padded)
- 🔄 **Entropy annealing** (0.02 → 0.005) for deterministic convergence
- 🎓 **Behavioral cloning warmup** on critical decision states
- 📊 **GRPO-compatible graders** for group-relative policy optimization

---

## 🚀 **Quick Start**

### **Option A: uv (Recommended)**

```bash
git clone https://github.com/keshav/MediFlow-RL.git
cd MediFlow-RL
uv sync
```

### **Option B: pip**

```bash
git clone https://github.com/keshav/MediFlow-RL.git
cd MediFlow-RL
python -m venv .venv
.venv\Scripts\activate  # Windows
# source .venv/bin/activate  # Linux/macOS
pip install -e .
```

### **Environment Variables**

```bash
cp .env.example .env
# Edit .env with your API keys (optional for LLM inference)
```

---

## 🎓 **Usage Examples**

### **1. Train a Policy**

```bash
# Phase 1: Easy/Moderate curriculum
python algorithms/ppo_training.py --phase 1 --seed 42

# Phase 2: Moderate/Hard curriculum (resumes from Phase 1)
python algorithms/ppo_training.py --phase 2 --seed 42

# Phase 3: Hard/Extreme curriculum
python algorithms/ppo_training.py --phase 3 --seed 42
```

### **2. Evaluate a Checkpoint**

```bash
python graders/basic_grader_eval.py \
  --model-path models/ppo_phase3.zip \
  --seed 42 \
  --eval-training-step 50000 \
  --deterministic
```

**Output:**
```
🟢 Easy      0.9974  ✅ PASS
🟡 Moderate  0.8899  ✅ PASS
🔴 Hard      0.7200  ✅ PASS
⚫ Extreme   0.5800  ✅ PASS
Overall:     0.7968
```

### **3. Run LLM or Heuristic Inference**

```bash
python inference.py --seed 42 --max-steps 220 --request-timeout 20
```

**Output:**
```json
{
  "success": true,
  "termination_reason": "all_delivered",
  "score": 0.847,
  "delivery_score": 0.90,
  "thermal_score": 0.82,
  "efficiency_score": 0.78
}
```

### **4. Start OpenEnv Server**

```bash
PYTHONPATH=. uvicorn server.app:app --host 0.0.0.0 --port 8000
```

---

## 📂 **Repository Structure**

```
MediFlow-RL/
├── 📁 algorithms/          # PPO training + phase callbacks
├── 📁 core/                # Simulation engine
│   ├── env.py              # Main Gymnasium environment
│   ├── config.py           # Configuration dataclass
│   ├── city_graph.py       # Graph builder + Dijkstra
│   ├── shipment.py         # Thermal physics (Newton's Law)
│   ├── vehicle.py          # Vehicle state machine
│   ├── weather.py          # Stochastic weather events
│   ├── reward.py           # Reward components
│   └── action_mask.py      # Legal action masking
├── 📁 graders/             # Four-tier evaluation suite
│   ├── easy_grader.py
│   ├── moderate_grader.py
│   ├── hard_grader.py      # Adversarial seeds
│   ├── extreme_grader.py   # Triage-weighted scoring
│   └── composite.py        # GRPO reward signal
├── 📁 evaluation/          # Deterministic rollout contracts
├── 📁 server/              # FastAPI + OpenEnv layer
├── 📁 tests/               # 30 unit tests
├── 📁 models/              # Training checkpoints
│   ├── ppo_phase1.zip
│   ├── ppo_phase2.zip
│   └── ppo_phase3.zip
└── 📄 inference.py         # LLM/heuristic policy runner
```

---

## 🧪 **Testing**

```bash
# Fast smoke tests (run before commits)
PYTHONPATH=. pytest tests/test_eval_contract.py tests/test_graders.py -q

# Full test suite (30 tests)
PYTHONPATH=. pytest tests/ -v
```

**Test Coverage:**
- ✅ API compliance
- ✅ Observation shape consistency
- ✅ Action mask correctness
- ✅ Reward hacking prevention
- ✅ Grader range enforcement [0,1]
- ✅ Adversarial scenario coverage
- ✅ Partial delivery reward shaping

---

## 🌐 **Deployment**

### **Validate Locally**

```bash
openenv validate . -v
```

### **Push to Hugging Face Space**

```bash
openenv push .
```

### **Live Demo**

🔗 **[https://huggingface.co/spaces/keshav/MediFlow-RL](https://huggingface.co/spaces/keshav/MediFlow-RL)**

---

## 🔬 **Why This Matters for RL Research**

MediFlow-RL addresses three **unsolved problems** in applied reinforcement learning:

### **1. Dual-Objective Optimization Under Physical Constraints**

Most logistics environments optimize for time alone. Cold chain requires **simultaneous minimization** of:
- ⏱️ Delivery time (customer satisfaction)
- 🌡️ Thermal excursion (product safety)

These objectives **frequently conflict**—and no single-objective policy can resolve the tension.

### **2. Reactive Behavior Under Stochastic Degradation**

The refrigeration state machine (Working → Degraded → Failed) tests whether agents understand **causal relationships**. 

Policies that ignore degrading refrigeration fail **100% of Hard/Extreme tier scenarios**, regardless of routing quality.

### **3. Triage Under Resource Scarcity**

**Extreme tier is designed so perfect agents cannot save all cargo.**

The question isn't "Can you deliver everything?"—it's:

> **"When forced to choose, do you sacrifice vaccines to save organs?"**

This is measured explicitly via **triage-weighted scoring**, not just delivery ratios.

---

## 📖 **Citation**

If you use MediFlow-RL in your research, please cite:

```bibtex
@software{mediflow_rl_2025,
  title   = {MediFlow-RL: Reinforcement Learning Environment for
             Pharmaceutical Cold Chain Logistics},
  author  = {Keshav},
  year    = {2025},
  url     = {https://github.com/keshav/MediFlow-RL},
  note    = {OpenEnv-compatible Gymnasium environment}
}
```

---

## 🤝 **Contributing**

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/ImprovementName`)
3. Commit changes (`git commit -m 'Add ImprovementName'`)
4. Push to branch (`git push origin feature/ImprovementName`)
5. Open a Pull Request

---

## 📜 **License**

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🌟 **Acknowledgments**

**MediFlow-RL** was developed to address a real-world humanitarian crisis: preventable pharmaceutical waste in global supply chains.

This project is dedicated to:
- 🏥 Healthcare workers in low-resource settings
- 🧬 Researchers working on vaccine logistics
- 🌍 Organizations fighting preventable diseases worldwide

---

<div align="center">

### 💫 **Developed with Passion by Keshav**

*Making cold chain failures a training problem, not a humanitarian crisis*

---

[![GitHub Stars](https://img.shields.io/github/stars/keshav/MediFlow-RL?style=social)](https://github.com/keshav/MediFlow-RL)
[![Twitter Follow](https://img.shields.io/twitter/follow/keshav?style=social)](https://twitter.com/keshav)

**[⭐ Star this repo](https://github.com/keshav/MediFlow-RL)** if you believe in saving lives through AI!

---

*"Technology should serve humanity's greatest challenges."* – Keshav

</div>
