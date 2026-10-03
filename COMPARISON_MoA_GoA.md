# Comparison: Graph-of-Agents (GoA) vs. Mixture-of-Agents (MoA)

While both frameworks aim to leverage multiple Large Language Models (LLMs) collaboratively to solve complex tasks, they differ significantly in architecture, orchestration, and how models interact.

## 1. Architecture & Structure

*   **Graph-of-Agents (GoA):**
    *   **Graph-Based:** Employs a dynamic, graph-based structure where models act as nodes and the relationships/communication between them are represented as weighted edges.
    *   **Dynamic Topology:** The interaction topology is not fixed. It is dynamically generated per task based on how models evaluate each other's responses.

*   **Mixture-of-Agents (MoA):**
    *   **Layered/Sequential:** Typically uses a layered or cascaded architecture (similar to a deep neural network) where a set of models in one layer generates responses that are fed to a "router" or the next layer of models.
    *   **Fixed Topology:** The structure (number of layers, models per layer) is generally pre-defined and static during inference.

## 2. Model Selection & Orchestration

*   **Graph-of-Agents (GoA):**
    *   **Node Sampling:** Dynamically selects a subset of relevant models (nodes) from a larger pool for the specific query.
    *   **Edge Sampling (Evaluation):** Models evaluate *each other's* initial responses. These evaluations form directed, weighted edges in the graph, representing the trust or relevance between models for the given task.
    *   **Message Passing:** Information flows along these weighted edges. Models refine their answers by considering the responses of other models they are connected to (those they scored highly).

*   **Mixture-of-Agents (MoA):**
    *   **Routing/Gating:** Often uses a gating network or a routing mechanism to select which models to activate for a given input, or runs all models in a layer and aggregates their outputs.
    *   **Aggregation:** Outputs from multiple models are typically aggregated (e.g., by a meta-model or through a voting mechanism) rather than models directly refining each other's answers through a peer-evaluation graph.

## 3. Communication Mechanism

*   **Graph-of-Agents (GoA):**
    *   **Peer-to-Peer:** Communication is essentially peer-to-peer, dictated by the dynamically formed graph. Models see and refine based on specific other models' outputs.

*   **Mixture-of-Agents (MoA):**
    *   **Hierarchical/Feed-Forward:** Communication is usually feed-forward from one layer to the next, often bottlenecked through a central aggregator or router.

## Summary

In essence, **MoA** organizes models in a structured, often layered, pipeline with routing and aggregation, whereas **GoA** creates an ad-hoc, collaborative graph where models dynamically select peers to learn from based on real-time peer evaluation.
