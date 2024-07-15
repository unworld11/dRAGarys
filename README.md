dRAGarys implements SelfRAG.

Self-RAG is a strategy for RAG that incorporates self-reflection / self-grading on retrieved documents and generations.


In the [paper](https://arxiv.org/abs/2310.11511), a few decisions are made:

1. Should I retrieve from retriever R
   - Input: x (question) OR x (question), y (generation)
      Decides when to retrieve D chunks with R
   - Output: yes, no, continue
2. Are the retrieved passages D relevant to the question x
   - Input: (x (question), d (chunk)) for d in D
      d provides useful information to solve x
   - Output: relevant, irrelevant
3. Are the LLM generation from each chunk in D is relevant to the chunk (hallucinations, etc) -
    - Input: x (question), d (chunk), y (generation) for d in D
All of the verification-worthy statements in y (generation) are supported by d
    - Output: {fully supported, partially supported, no support
4. The LLM generation from each chunk in D is a useful response to x (question) -
    - Input: x (question), y (generation) for d in D
y (generation) is a useful response to x (question).
    - Output: {5, 4, 3, 2, 1}

