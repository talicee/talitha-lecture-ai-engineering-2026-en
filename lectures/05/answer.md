# Lecture 05 Answers

## Exercises

- Answering model (`[model]` shown during execution): Gemini 3.5 Flash-Lite
- Comparison question: In Lecture 2, what does LoRA freeze and what does it train? What does QLoRA add?
- Target materials (also record the difference in scope between full context and the other methods): Lectures 1–3 main lecture materials for Vector Search, Tree, and Graph (214 pages). Full Context used all 9 documents (438 pages).

### Results by Method

| Method | Key points and correctness of the answer | Cited pages and evidence | Time (seconds) | Input/output tokens | Model responses | Estimated generation API cost (USD) |
|---|---|---|---|---|---|---|
| Full context | Correct. LoRA freezes original weights and trains low-rank adapter matrices. QLoRA adds 4-bit compression of the base weights. | Lecture 2, pp. 75 and 81 (as cited in the answer). | 5.42 | 95,823 / 132 | 1 | $0.029077 |
| Vector search | Correct. LoRA freezes original weights and trains small low-rank matrices A and B. QLoRA compresses base weights to 4-bit. | Lecture 2, pp. 51–52. Retrieved `lec02-main-p052` as relevant evidence. | 3.08 | 2,757 / 169 | 2 | $0.001250 |
| Tree | Correct. LoRA freezes original weights and trains low-rank matrices A and B. QLoRA adds 4-bit quantization to reduce memory requirements. | Lecture 2, p. 52 (`lec02-main-p052`), reached through the section *When and how to adapt the selected model*. | 6.02 | 9,437 / 317 | 5 | $0.003624 |
| Graph | Correct. LoRA freezes original weights and trains low-rank matrices A and B. QLoRA adds 4-bit quantization to reduce memory usage. | Lecture 2, pp. 51–52 (as cited in the answer); search returned seed `lec02-main-p052`. | 10.80 | 5,186 / 239 | 2 | $0.002153 |

<!-- State when a method was not run or a cost was unavailable. Use a separate table for each additional question. -->

- Pages found by running search alone, and what their text confirmed:
  - `lec02-main-p052` (Lecture 2, p.52): Directly confirmed that LoRA freezes original weights and trains a small change (delta), while QLoRA compresses the original weights to 4-bit.
  - `lec02-main-p051` (Lecture 2, p.51): Related explanation of PEFT and training only part of a model.
  - `lec02-main-p060` (Lecture 2, p.60): Exercise related to QLoRA and measuring fine-tuning effects.
  - `lec02-main-p079` (translated PDF p.79): Discussion of RAG versus fine-tuning for adding knowledge.
  - `lec02-main-p061` (Lecture 2, p.61): Exercise instructions and deliverables.
  - Page 52 was the most directly relevant evidence for the comparison question.

- Tool calls shown by `--trace` (names, arguments, counts, table-of-contents paths followed by Tree, etc.):
  - Vector search: `search_materials({'query': 'LoRA freeze train QLoRA add'})` — 1 tool call. Retrieved relevant Lecture 2 material, including `lec02-main-p052`.
  - Tree: `browse_tree({})` → `browse_tree({'node_id': 'lec02-main'})` → `browse_tree({'node_id': 'lec02-main-s045'})` → `browse_tree({'node_id': 'lec02-main-p052'})` — 4 tool calls. Navigated from the course root to Lecture 2, then to the relevant section, and finally to page 52.
  - Graph: `search_graph({'query': 'LoRA freeze train QLoRA add Lecture 2'})` — 1 tool call shown. Returned `lec02-main-p052` as a seed page.

- Examples where retrieved information was insufficient, or was retrieved but not used in the answer:
  - No obvious insufficiency was observed in this test. All four methods produced a correct answer to the comparison question.
  - Vector search retrieved additional pages that were related to fine-tuning and RAG but were not necessary to answer the question directly.
  - The comparison was limited to a single question, so it does not establish how each method performs when information must be combined across multiple pages or lectures.


- Method you would adopt for this use case, your reasons, and limitations of the comparison conditions:
  - I would adopt Vector RAG for this use case so far, due to its lower token usage, cost, and response time. However, Tree or Graph retrieval may be more suitable for structured documents such as company guidebooks, technical manuals, and legal documents, where hierarchical navigation or cross-document relationships are important. This comparison was limited to one question and one run per method, with different material scopes.

- Observations and questions:
  - Vector RAG was the most efficient in this test.
  - Tree and Graph approaches may be more useful for structured or interconnected knowledge, such as guidebooks, manuals, and regulations.
  - Could a hybrid approach combining vector search with hierarchical or graph retrieval provide better results?

## Homework

<!-- Completing any one of Basic, Implementation, or Advanced is sufficient. -->

- Level attempted: Basic 
- What you did (files, settings, or processing changed, or retrieval method designed):
  - Changed `RAG_TOP_K` in `app/config.py` from `5` to `8`, increasing the number of chunks retrieved by Vector RAG.
  - No other files, settings, or processing logic were modified.

- Comparison question and conditions held fixed (model, target materials, etc.):
  - Question: "In Lecture 2, what does LoRA freeze and what does it train? What does QLoRA add?"
  - Model: `gemini-3.5-flash-lite`.
  - Target materials: Lecture 1–3 main materials (same retrieval index).
  - The question, model, and retrieval method were held fixed; only `RAG_TOP_K` was changed from 5 to 8.

- Results (answers and evidence before/after, `--trace` output, time, token counts, estimated generation API cost, etc.):
  - Both K=5 and K=8 produced correct answers:
    - LoRA freezes the original model weights and trains small low-rank matrices (A and B).
    - QLoRA additionally compresses the original weights to 4 bits.
  - Both runs retrieved the directly relevant Lecture 2 page (`lec02-main-p052`) through `search_materials`.
  - **K=5 (before):**
    - Time: 3.08 seconds
    - Input tokens: 2,757
    - Output tokens: 169
    - Model responses: 2
    - Estimated API cost: $0.001250 USD
  - **K=8 (after):**
    - Time: 14.09 seconds
    - Input tokens: 4,017
    - Output tokens: 186
    - Model responses: 2
    - Estimated API cost: $0.001670 USD
  - Standalone retrieval results showed that the first two results (Lecture 2 pp. 51–52) contained sufficient evidence to answer the question, while the remaining results provided mostly supplementary or indirectly related information.
  - Increasing K from 5 to 8 did not visibly improve answer correctness, but increased input token usage and estimated generation API cost. The latency also increased in this run, although a single run is insufficient to establish a consistent latency difference.
  - **Insight:** For this question, K=5 appeared sufficient. Retrieving more chunks did not visibly improve the answer and introduced additional context and cost. However, this is an observation from a single question and run per setting, rather than a general conclusion about the optimal retrieval size.
- Examples of improvements and remaining failures or limitations:
  - The retrieved evidence suggests that fewer chunks might also be sufficient, since the first two results (Lecture 2 pp. 51–52) contained the information needed to answer the question.
  - However, K<5 has not yet been tested, so its effect on answer quality, retrieval relevance, and cost remains unknown.
  - The experiment was limited to one question and one run per setting, making the results preliminary.
- Observations and questions:
  - Increasing RAG_TOP_K from 5 to 8 increased input token usage and estimated generation API cost without visibly improving answer correctness.
  - Could reducing RAG_TOP_K to 3 or fewer still retrieve sufficient evidence to answer correctly while reducing token usage and cost?
  - Does a higher RAG_TOP_K become more beneficial for questions that require information from multiple pages, rather than a single directly relevant page?


- AI tools used:
  - Used ChatGPT to help analyze and interpret the experiment outputs, compare the results between K=5 and K=8, and organize the observations and conclusions.
  - Ran the commands and experiments myself, and verified the outputs, retrieval results, token usage, execution time, and estimated costs from the terminal.
