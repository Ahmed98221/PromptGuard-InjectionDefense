
📄 README.txt
📘 PromptGuard: A Structured Defense Framework for Injection-Resilient Language Models

📌 Title
PromptGuard – A Structured Defense Framework for Injection-Resilient Language Models

📖 Description
PromptGuard is a lightweight, multi-layered defense framework designed to protect large language models (LLMs) such as GPT-4, Claude 3, and LLaMA 2 from prompt injection attacks. It integrates four core components:
1. Input Filtering,
2. Structured Prompt Formatting,
3. Output Validation, and
4. Adaptive Response Refinement (ARR).

Unlike single-layer or retraining-based approaches, PromptGuard is model-agnostic, easy to deploy, and retraining-free. It provides strong resilience against both syntactic and semantic injection attacks with minimal latency overhead.

📂 Dataset Information
This framework supports the following standard evaluation datasets:

- InjectBench: A benchmark suite for injection prompts.
- InjectGuard: Targeted attacks for injection bypass scenarios.
- TruthfulQA: For output alignment evaluation and hallucination reduction.

Please ensure to download these datasets separately from their respective repositories:
- InjectBench: https://github.com/thunlp/InjectBench
- TruthfulQA: https://github.com/sylinrl/TruthfulQA

Place datasets in a directory named ./data/ following the structure expected in datasets.py.

🧠 Code Information

| File | Description |
|------|-------------|
| config.py | Contains global configurations and file paths |
| datasets.py | Dataset loader functions for InjectBench, InjectGuard, and TruthfulQA |
| layer1_input_filtering.py | Implements regex and BERT-based hybrid input filtering |
| layer2_structured_format.py | Applies structured prompt formatting to sanitize inputs |
| layer3_output_validation.py | Validates model output using LLM-as-a-Critic |
| layer4_response_refine.py | Refines unsafe outputs using adaptive correction |
| pipeline.py | Full defense pipeline chaining all four layers |
| utils.py | Utility functions (e.g., logging, metrics) |
| run_experiment.py | Main script to run evaluation and generate metrics |

▶️ Usage Instructions

1. Install Dependencies
   Use the following command to install required libraries:
   pip install -r requirements.txt

2. Download Datasets
   Download datasets mentioned above and place them in ./data/.

3. Run Evaluation
   python run_experiment.py

4. Expected Output
   Evaluation metrics such as F1-score, injection success rate, and output alignment accuracy will be displayed in the console and saved in logs.

📦 Requirements

- Python version: 3.8+
- Dependencies:
  - transformers
  - scikit-learn
  - openai (or relevant LLM API)
  - torch
  - regex
  - tqdm

You can install these with:
pip install transformers scikit-learn torch regex tqdm openai

🧪 Methodology

PromptGuard’s pipeline is composed of the following:

1. Layer 1 – Input Filtering
   Uses pattern-matching (regex) and semantic filtering (BERT classifier) to detect potential injection attempts in incoming prompts.

2. Layer 2 – Structured Prompt Formatting
   Reformats prompts using predefined safe templates to prevent injection merging or override.

3. Layer 3 – Output Validation
   Uses a secondary LLM to verify whether the model output aligns with the original instruction and doesn’t reflect injected behavior.

4. Layer 4 – Adaptive Response Refinement (ARR)
   If validation fails, this module iteratively refines the response while maintaining instruction intent.

📊 Metrics Used

- F1-Score: For prompt injection classification accuracy
- Injection Success Rate: Percentage of successful prompt injections bypassing the defense
- Output Alignment Accuracy: Whether the LLM response adheres to the original user intent
- Latency Overhead: Additional delay introduced by the defense pipeline

📚 Citations

If you use this code or methodology in your research, please cite:

@article{alzahrani2025promptguard,
  title={PromptGuard: A Structured Defense Framework for Injection-Resilient Language Models},
  author={Ahmed Alzahrani},
  journal={Scientific Reports},
  year={2025},
  note={Available on request}
}

⚖️ License & Contribution

- This repository is released under the MIT License.
- Contributions are welcome via pull requests.
- For major changes, please open an issue first to discuss what you would like to change.
