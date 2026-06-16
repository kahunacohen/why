# why
Project: why — AI-assisted investigation framework

  The goal is an investigation framework where reasoning state lives in a typed graph, not in an LLM context window. LLM context is bad state — ephemeral, opaque, unrepeatable. The graph externalizes that
  state so the AI becomes a stateless function: (current_graph, new_input) → graph_update. The AI reads the graph, proposes typed additions, commits them. No conversation history needed between steps. The
  graph IS the investigation.

  Data model (already sketched in diagrams/medical.mmd):

  - Node types: Observation, Action, Hypothesis
  - Edge types: motivates (Obs→Action), produces (Action→Obs), suggests (Obs→Hyp)

  The schema enforces the grammar of investigation — the type system rules out nonsensical connections.

  Value: The completed graph is a reasoning receipt — auditable, replayable, forkable. Given the same observations, the graph structure is deterministic even if LLM prose varies.

  Language: OCaml. Algebraic data types are the natural fit for typed nodes/edges. Pattern matching is exhaustive — the compiler enforces completeness on traversal. GC removes a problem that isn't relevant at
  this scale. The functional paradigm (immutable by default, recursion over loops) is genuinely new territory from Go/TS. Rust and Zig were ruled out: manual memory management adds friction without payoff for
  a graph of this size.

  Working style: User writes the code, AI reviews only.
