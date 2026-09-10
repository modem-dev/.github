# Context Graph as Infrastructure — Visual Storyboard & Prompt Pack

A production kit for two mirrored looping visuals and a ~75-second explainer video,
built to feed a generative video tool (Runway Gen-4, Luma, Kling, Veo). Visual A shows
an agent working against an LLM alone. Visual B shows the same loop with a context
graph as an infrastructural layer between the agent and the LLM.

---

## 1. The mechanism (what the visuals must get right)

Before art direction, the technical story — this is what the motion has to encode
honestly:

**Without a context graph (Visual A):**

1. A person or agent submits a prompt with little organizational context attached.
2. The LLM receives it "cold." To compensate, the agent loop does blind searching:
   repeated retrieval calls, tool calls, and re-prompts, with the growing context
   re-sent on every round trip.
3. Each round trip adds latency and tokens. Industry traces show the majority of
   input tokens are spent re-sending instructions, policies, and tool descriptions
   on every call — overhead, not work.
4. The answer that finally returns is slower, more expensive, and often generic,
   because the model never saw how the org's facts connect (who owns what, what
   depends on what, what customers actually said).
5. Downstream effect: people stop trusting the answers, fewer people adopt the
   tools, and the whole org works more slowly.

**With a context graph (Visual B):**

1. The same prompt is submitted — but it first passes through the context graph
   layer sitting between the agent and the model.
2. The graph resolves the entities in the request (this customer, this service,
   this feature, this team) and traverses their relationships **deterministically —
   no LLM calls at retrieval time**, so this step is fast and near-zero token cost.
3. The request arrives at the LLM already carrying execution-ready context: the
   relevant facts *and how they connect*. Relational grounding, not a pile of
   similar-looking documents.
4. The LLM does one clean pass instead of an iterative search loop. Fewer round
   trips, fewer tokens, faster wall-clock, and answers grounded in the org's
   actual state.
5. Because the layer is shared infrastructure, every agent draws from it —
   engineering, support, customer success — and the same speedup compounds
   across the org. Relevant answers → more adoption → more people activated.

**The honest claim** (important for the script): the context graph doesn't replace
the LLM's reasoning — it replaces the *blind searching around* the LLM. The model
still thinks; it just stops guessing where the facts are.

---

## 2. Art direction — infrastructure, not dot clouds

**The one rule:** the context graph is never rendered as a floating node-and-edge
dot cloud. It is rendered as *built infrastructure* — a load-bearing stratum. The
only permitted "graph-y" moment is a sub-second macro shot where the surface of the
layer resolves into a crystalline lattice — the molecular structure of the
infrastructure — before pulling back to read as solid again.

**Visual metaphor:** a cross-section of a system, like an architectural elevation
or a cutaway of a datacenter/substrate:

- **The agent origin** — a small, warm point of light at the left edge (a terminal
  card / workstation glyph). Human-scale.
- **The LLM** — a large monolithic core at the right edge: a dense, slowly
  breathing volume of light. Powerful but opaque.
- **The context graph (Visual B only)** — a wide horizontal stratum spanning the
  frame between them: a slab of dark glass with fine etched circuitry, like a
  silicon interposer or an illuminated foundation plate. Calm, precise,
  load-bearing. It doesn't float — it *supports*.
- **Data** — pulses of light traveling along conduits. A pulse's brightness,
  color-density, and mass encode how much useful context it carries.

**Palette:** near-black background (#0A0E14), cool graphite structures, one warm
accent for the prompt/agent (amber), one cool accent for the model (cyan/blue),
and a distinct signature color for the context graph stratum (electric teal or
Modem brand color). Response pulses in Visual B blend agent-warm + graph-teal to
show the answer carries context.

**Motion language:** Visual A is jittery, iterative, wandering — motion that
doubles back. Visual B is laminar, single-pass, confident. The two loops are
composed as mirrors: same camera, same framing, same left/right anchors, so a
side-by-side cut makes the difference legible instantly.

**Type (if any):** minimal HUD labels only — `PROMPT`, `LLM`, `CONTEXT GRAPH`,
a token counter, a timer. No paragraphs on screen.

---

## 3. Visual A — the loop without a context graph (~10s seamless loop)

| # | Time | Shot | Action |
|---|------|------|--------|
| A1 | 0.0–1.5s | Wide cross-section, locked camera | Dark frame. Left: small warm terminal glyph pulses — a prompt is born as a single amber pulse. It launches rightward along a thin conduit. |
| A2 | 1.5–3.0s | Same wide | The pulse crosses a long stretch of *empty* dark space — nothing between origin and model — and enters the large cyan LLM core on the right. |
| A3 | 3.0–6.5s | Slow push-in on the core | Inside, the pulse fractures into many thin strands that wander and probe dark volume — searching blindly. Two or three faint echo pulses fire *back* to the origin and return (re-prompts). A small token counter climbs fast; a timer stretches. The core churns visibly — lots of motion, little progress. |
| A4 | 6.5–8.5s | Pull back to wide | A single dim, pale response pulse finally exits the core and crawls back left along the conduit — noticeably slower and dimmer than the outbound prompt. |
| A5 | 8.5–10.0s | Wide | The dim pulse arrives at the terminal glyph, which flickers uncertainly (a mediocre answer). Frame settles to the exact state of A1's first frame. **Loop point.** |

**Feeling:** effort without traction. The machine is powerful but starved.

---

## 4. Visual B — the loop with the context graph (~10s seamless loop, mirrored)

| # | Time | Shot | Action |
|---|------|------|--------|
| B1 | 0.0–1.5s | Identical wide framing to A1 | Same terminal glyph, same amber prompt pulse launches. But now a wide teal stratum — a slab of etched dark glass — spans the gap between agent and LLM, seated like a foundation layer. It idles with a faint, steady circuit-glow. |
| B2 | 1.5–3.0s | Wide → brief macro insert (~0.7s) | The pulse enters the stratum. **The one permitted graph moment:** an extreme close-up where the slab's surface resolves into a crystalline lattice — the molecular structure of the layer — with exactly the relevant channels lighting up in sequence (entity → relationship → relationship). Snap back to wide before it can read as a "network diagram." |
| B3 | 3.0–4.5s | Wide | The pulse exits the stratum transformed: larger, denser, now amber-wrapped-in-teal — the prompt carrying its context. It travels the short remaining run into the LLM core. |
| B4 | 4.5–6.5s | Push-in on the core | One clean event: the core brightens in a single coherent flash — one pass, no wandering strands, no echo round-trips. The token counter barely moves; the timer barely advances. |
| B5 | 6.5–8.5s | Pull back to wide | A bright, saturated response pulse exits immediately and travels back left — faster and brighter than the outbound prompt. As it re-crosses the stratum, the slab gives a subtle acknowledging shimmer (the layer also learns/updates). |
| B6 | 8.5–10.0s | Wide | The response lands; the terminal glyph blooms confidently. Optionally, 2–3 sibling terminal glyphs (other teams' agents) glow faintly along the same stratum — same infrastructure, many consumers. Settle to B1's first frame. **Loop point.** |

**Feeling:** the same machine, now standing on a foundation. Calm speed.

**Side-by-side cut:** because A and B share framing and timing, a split-screen loop
works with zero re-editing: A is still churning at 6s while B's answer is already
home. That single frame *is* the pitch.

---

## 5. Runway / gen-video prompt pack

**How to use:** generate 5–10s clips per shot (image-to-video from a styleframe
gives far more control than text-to-video — generate stills of the wide
composition first, then animate). For seamless loops, use first-frame + last-frame
keyframes set to the same still. Assemble shots in an editor; gen tools rarely nail
a 10s multi-beat sequence in one generation.

**Style anchor — prepend to every prompt:**

> Minimal futurist infrastructure diagram brought to life, cinematic 3D render,
> architectural cross-section on a near-black background, dark graphite
> structures, glowing light pulses traveling along thin conduits, amber and cyan
> accent lighting, ultra-clean composition, locked-off camera, shallow haze,
> premium tech-brand aesthetic, 4K, no text.

**Negative / avoid (append or use negative prompt field):**

> no floating point-cloud networks, no node-and-edge dot graphs, no particle
> swarms, no neurons, no human faces, no UI screenshots, no text or letters.

**Shot prompts:**

- **A1/A2 (prompt travels alone):** "A single warm amber pulse of light is born at
  a small terminal module on the far left and travels right along one thin conduit
  across a vast empty dark gap, toward a huge monolithic cube of dim cyan light on
  the far right, wide static shot."
- **A3 (blind searching):** "Inside a vast dark monolithic core, one amber light
  strand splits into many thin wandering filaments that probe and double back
  through dark empty volume, chaotic searching motion, occasional faint pulses
  firing backward out of frame, restless energy, slow camera push-in."
- **A4/A5 (weak response):** "A single dim pale pulse of light slowly exits a
  large cyan core and crawls left along a thin conduit toward a small terminal
  module, sluggish motion, the module flickers weakly on arrival, wide static
  shot."
- **B1 (the stratum, establishing):** "Between a small terminal module on the left
  and a monolithic cyan core on the right, a wide horizontal slab of dark etched
  glass spans the frame like a load-bearing foundation layer, fine teal circuitry
  glowing steadily inside it, monumental and calm, architectural cross-section,
  wide static shot."
- **B2 (macro lattice — the only 'molecular' moment, keep the clip under 1s in
  edit):** "Extreme macro shot of a dark glass surface resolving into a precise
  crystalline lattice, a chain of facets lighting up in rapid sequence like a
  signal routing through crystal, teal light, shallow depth of field, 0.7 seconds
  of screen time."
- **B3 (enriched prompt):** "An amber pulse of light emerges from a glowing teal
  glass stratum transformed: larger, denser, wrapped in a teal sheath, and glides
  smoothly right into a monolithic core, confident laminar motion, wide static
  shot."
- **B4 (single clean pass):** "A monolithic cyan core receives a bright
  amber-teal pulse and brightens once in a single coherent flash, no internal
  churning, immediate and decisive, slow push-in."
- **B5/B6 (fast grounded response):** "A bright saturated pulse of light travels
  quickly leftward along a conduit, crossing a glowing teal glass stratum that
  shimmers in acknowledgment, and lands at a small terminal module which blooms
  with steady light; two sibling modules along the same stratum glow faintly,
  wide static shot."
- **Split-screen beauty shot (social cut):** "Split screen of two identical dark
  infrastructure cross-sections: top half, a lone pulse wanders chaotically inside
  a large core; bottom half, a pulse crosses a glowing teal foundation layer and
  returns home bright and fast, synchronized start, mirrored composition."

---

## 6. Explainer video script (~75s)

| Beat | VO | Visual |
|------|----|--------|
| 1 (0–8s) | "Every AI answer starts the same way: a prompt leaves an agent and travels to a model." | Visual A1–A2. |
| 2 (8–18s) | "But the model doesn't know your org. So it searches blind — retrieving, re-prompting, resending everything it already knew, burning tokens on every round trip." | Visual A3, token counter climbing. |
| 3 (18–26s) | "The answer comes back slow. And generic. Do that across a whole company and everything drags — engineering, support, customer success. People stop trusting the answers, so they stop using them." | A4–A5; pull wide to an org grid of terminal glyphs, most of them dark. |
| 4 (26–36s) | "Now add one layer. A context graph — infrastructure that sits between your agents and the model." | B1: the stratum slides into place beneath the same scene, like a foundation being set. |
| 5 (36–48s) | "Before the prompt reaches the model, the graph attaches what matters: this customer, this service, this decision — and how they connect. No blind searching. The model gets the question *and* the ground truth, in one pass." | B2 macro lattice (<1s) → B3 → B4. |
| 6 (48–58s) | "So the answer comes back fast, grounded, and cheap — fewer round trips, fewer tokens, more work done in the same hour." | B5; side-by-side split with A still churning. |
| 7 (58–70s) | "And because it's infrastructure, every agent stands on it. Engineering speeds up. Support speeds up. Answers get relevant, so people actually adopt — while competitors are still re-prompting." | Org grid again: glyph after glyph lighting up along the shared stratum. |
| 8 (70–75s) | "The model is the engine. The context graph is the ground it runs on. **Modem — the context layer for your customer.**" | Final locked wide of Visual B looping; logo. |

---

## 7. Research notes & claim hygiene

Grounding for the claims the visuals make:

- **Context layer as a category:** the industry now describes a "context layer" as
  infrastructure sitting between operational systems and agents, turning scattered
  data into structured, relationship-aware, execution-ready context — and frames
  most agent failures as *context* failures, not model failures
  ([Atlan](https://atlan.com/know/context-layer-for-ai-agents/),
  [Tellius](https://www.tellius.com/resources/blog/what-is-a-context-layer-for-ai-agents-the-definitive-guide-for-2026)).
- **Token waste in the baseline loop:** analyses of production LLM traces find the
  large majority of input tokens (~69% in one study) are spent re-sending
  instructions, policies, and tool descriptions on every call
  ([Atlan](https://atlan.com/know/why-ai-agents-need-an-enterprise-context-layer/)).
- **Why graph-shaped context wins:** graph retrieval gives the model *how facts
  connect* rather than piles of similar text, and structured/graph retrieval can
  cut context size and token usage substantially (up to ~80% in vendor-reported
  cases) ([PuppyGraph](https://www.puppygraph.com/blog/graphrag-knowledge-graph),
  [Graphwise](https://graphwise.ai/blog/building-smarter-faster-how-graphrag-cuts-ai-development-costs-and-complexity/)).
- **Retrieval-time efficiency:** graph-based retrieval methods (LightRAG,
  HippoRAG2, GFM-RAG) avoid LLM calls at retrieval time — zero retrieval-token
  overhead versus iterative agentic retrieval that re-prompts the model per hop
  ([survey](https://arxiv.org/pdf/2506.05690), [LightRAG results via
  arXiv](https://arxiv.org/html/2508.06105)).
- **Caveat to keep us honest:** *naive* GraphRAG implementations that summarize
  the graph with an LLM at query time can be slower, not faster. The speed story
  holds when traversal is deterministic and pre-indexed — which is exactly the
  "infrastructure, not on-the-fly searching" framing. Don't claim "the LLM does no
  work"; claim "the LLM stops searching blind."
- **Modem's framing:** a customer context graph built from ingested messages and
  events, unified user/company profiles, an entity schema that makes agent
  questions answerable, positioned against plain vector similarity search
  ("similarity search alone leaves agents answering generically") —
  modem.dev/guides.
