---
name: n8n-tidy-up
description: Arrange existing n8n workflows into beautiful compact box-shaped layouts through MCP, with wrapped rows, readable branches, and grouped AI helpers while preserving behavior. Use for node placement, canvas cleanup, or workflow layout requests.
---

# n8n Tidy Up

Make the workflow feel deliberately designed and easy to trace at a glance. A uniform grid or n8n's built-in tidy command alone is not a finished result. Preserve behavior, then optimize composition. Default to actually saving the requested layout through MCP; honor preview-only requests.

## Artistic direction

Approach the canvas as a visual designer composing a diagram. The user wants artistic judgment, not mechanical packing. Use the box-shaped footprint as a compositional guide, with freedom to vary row lengths, spacing, and grouping when that improves the whole.

- Establish a visual story: a clear entry, recognizable stages, and an obvious finish. Make the eye follow the same journey as the workflow.
- Create rhythm through repeated alignments and spacing, with deliberate larger pauses between stages. Avoid making every gap identical when the semantic relationships differ.
- Balance visual weight: a dense agent cluster may need more whitespace than a simple chain. Judge the apparent size of labels, helpers, and notes, not just node counts.
- Use negative space intentionally to separate ideas and let complex regions breathe. Compact means composed, not squeezed.
- Prefer optical balance over forced symmetry. A short final row can sit naturally beneath the preceding stage; do not stretch it merely to touch both sides of the box.
- Treat wires as part of the composition. Reduce tangles, avoid connections cutting through unrelated groups, and leave clear corridors for row returns within the editor's routing limits.
- Keep decoration restrained and purposeful. Artistic quality should come from placement, proportion, hierarchy, and clarity. Add colors, frames, or annotations only within the user's requested scope.

Before choosing positions, mentally compare two plausible compositions: where to break rows, which clusters to keep together, and how to distribute visual weight. Choose the one that best combines readable flow, a balanced rectangular silhouette, and spacious local detail. Do not burden the user with options unless a meaningful preference is unresolved.

Critique the result like a designer: Where does the eye get lost? What feels cramped or stranded? Is any gap accidental? Does a row break interrupt an idea? Refine those issues rather than accepting a mathematically regular layout. Behavioral invariants remain hard constraints on artistic freedom.

## Preferred style: a compact box

The user's preferred composition is a rectangular footprint containing several balanced rows, like a neatly composed page. Each row reads left to right, and the end of one row connects to the start of the next. Avoid a long single-line workflow. The reference drawing shows three rows with approximately three nodes each; this illustrates wrapping and balanced use of space, not a fixed node count or mandatory square aspect ratio.

Choose a sensible row capacity from actual node widths, graph structure, labels, and helper clusters. Start with roughly 3–5 ordinary nodes per row and adjust to keep a compact landscape or near-square footprint. Prefer row breaks at logical stage boundaries. Balance row widths and outer margins without inserting fake nodes or stretching gaps. Reserve more vertical space between rows for return connections and AI helpers than between ordinary parallel lanes. Keep every row left-to-right by default; do not alternate direction just to create a snake.

Treat splits, joins, loops, and agent/helper clusters as coherent blocks when packing rows. Preserve execution-sensitive ordering even when it prevents ideal wrapping; leave such a block intact and explain the limitation. A rectangular footprint is the priority aesthetic, not a requirement to pack every node into identical cells.

The reference's outer box expresses the overall composition. Do not automatically create a literal border or a giant sticky note; add a frame only if requested. Position-only MCP edits cannot guarantee the reference's right-angled perimeter wires. Inspect actual n8n rendering when possible, and choose row spacing/breaks that make return edges readable without adding routing nodes or changing connections.

## Connect and scope

- Discover available n8n MCP tools and inspect their actual schemas. Find full workflow retrieval and updates supporting node positions. Never invent tool names or arguments. Documentation/search/execution access alone is insufficient to edit layout.
- Resolve the user's workflow URL or ID, or search by name. Ask for selection only when the target remains ambiguous. Scope changes to that workflow or the selected nodes.
- If no suitable MCP connection exists, explain that a server with full workflow read and node-position update capabilities must be connected. Do not silently substitute browser editing or direct API calls. A supplied JSON can support a local proposal, but is not a live MCP update.
- Read the complete workflow, connections, settings, node types, positions, existing notes and any version marker. Do not reconstruct a workflow from a summary. Keep a before snapshot in a dedicated task folder within the owning project; treat its contents as sensitive and do not commit it or print credentials.

## Preserve behavior, including placement-dependent behavior

Only node positions may change by default. Preserve IDs, names, types, versions, parameters, credentials, expressions, node array order, connections and their array order/indices, settings, pinned data, disabled flags, and activation/publication state. Do not execute, activate, publish, rename, delete, reconnect, or add executable nodes.

**Position can affect execution.** n8n's v1 branch ordering uses canvas height and then horizontal position. Record the original relative order of competing branch starts and preserve it in the new layout, including same-height left/right ties. Check this at every split, including nested splits. Never swap branches merely to place true above false. Keep tied positions tied where their tie-breaking semantics are unknown. When execution settings or competing branches are uncertain, preserve original coordinate ordering more conservatively or leave that region in place. Do not claim unchanged behavior solely because connections are unchanged.

Reference: [n8n execution order](https://docs.n8n.io/flow-logic/execution-order/). Check current documentation or server semantics when handling an unfamiliar execution mode.

Existing sticky notes may move with the nodes they describe. Preserve their text, color, and size by default. If the user requests section framing or annotations, resizing existing notes and adding a small number of descriptive notes is allowed; keep those changes separate from executable node parameters. Do not add decorative notes merely to fill space.

## Compose the canvas

First understand the graph: triggers, main execution paths, splits, joins, loop-back edges, disconnected components, AI model/tool/memory attachments, and existing semantic sections. Separate execution edges from auxiliary AI connections. Inspect connection types instead of assuming every edge runs left to right.

Use these as adaptable design defaults, not a rigid grid:

- **Reading direction:** triggers at the upper left; each row progresses rightward, wrapping to the left of the next row. Keep short sequences on one baseline within a row. Align equivalent stages in columns when it improves tracing.
- **Spacing:** start around 280–340 canvas units between ordinary node centers and 200–260 between branch lanes. Increase gaps for long labels, large nodes, crowded ports, or multiple helper rows. Use a consistent 20-unit rhythm where compatible with execution-order constraints. These are design heuristics, not assumed node dimensions.
- **Hierarchy:** choose a clear main path; give parallel alternatives distinct horizontal lanes. Allocate each branch enough vertical space for its entire subtree before placing adjacent branches. Short branches should not be stretched to match every step of a long one.
- **Splits and joins:** preserve branch order; keep branch starts in a consistent column and joins after all incoming paths. Favor compact, legible convergence over perfectly symmetrical but sprawling arrangements. Do not force branch order to match labels or output indices.
- **AI clusters:** place models, memory, parsers, and tools below their owning agent/chain, near the relevant attachment ports. Use a tidy row or two with clear gaps. Reserve this area so the next execution branch cannot run through it. Shared helpers sit between their consumers where practical; never duplicate nodes.
- **Loops:** keep the forward body readable and reserve outer whitespace for return connections. Preserve the distinction between loop body and exit. Do not break cycles or insert routing nodes to fake cleaner wires.
- **Sections:** move existing note-backed groups as coherent regions. Keep comfortable margins around their contents and avoid unrelated nodes inside a section. Use understated grouping, not a rainbow of oversized backgrounds.
- **Disconnected flows:** arrange separate components as distinct islands with consistent margins. Avoid scattering lone nodes through the main path. Preserve any position-sensitive ordering across components when applicable.
- **Wire clarity:** reduce crossings and long diagonals by moving nodes. Do not modify connections to eliminate crossings. The editor controls edge routing; do not promise perfectly straight or manually routed edges through position updates alone.
- **Overall balance:** favor the compact box composition with balanced wrapped rows. Avoid huge empty rectangles, cramped helper clusters, excessive width, and an unnecessarily tall staircase. Keep the result clear at overview zoom and comfortable at normal editing zoom. Wrap deliberately at logical boundaries rather than leaving a long horizontal chain.

For a selected region, keep outside nodes fixed and give boundary connections room. Prefer already-good placement over gratuitous movement. Honor specific user style preferences while retaining the behavioral constraints.

## Review and apply

1. Build a concrete ID-to-position plan from the complete snapshot. Check finite coordinates, unique node IDs, label clearance, branch lane separation, group bounds, and branch ordering. Estimate node footprints conservatively if exact dimensions are unavailable; distinguish estimates from observed rendering.
2. Review the whole composition a second time: follow each trigger to its endpoints, then trace each split, merge, loop, and AI attachment. Adjust awkward bottlenecks, unnecessary whitespace, and wire crossings where constraints permit. Avoid stopping at the first mechanically valid layout.
3. Compare the proposed workflow against the snapshot. Except for allowed layout/annotation fields, user-controlled workflow content must be identical. Prepare a reverse position map for recovery.
4. Re-read before writing. If the workflow changed since the snapshot, recompute against the fresh version rather than overwriting edits. Use optimistic concurrency if the server supports it.
5. Prefer a minimal batch update keyed by stable node IDs with position fields only. Use full replacement only if the documented tool requires it, the complete editable data is available, and unrelated fields can be preserved. Do not send masked/redacted credentials back as real values. Use dry-run validation if available; do not run the workflow as a layout test.
6. Apply the authorized layout. Do not ask for redundant approval when the user asked to tidy that workflow. After an ambiguous timeout, read current state before retrying. For partial failures, reconcile actual positions and retry only the missing layout changes once; stop and report if that still fails. Never blindly restore a stale full workflow over newer edits.
7. Fetch the saved workflow and verify planned positions, branch ordering, and all non-layout invariants. Ignore only documented server-managed bookkeeping differences such as modification timestamps or version IDs. Treat unexpected changes as a failure needing inspection.
8. If an MCP canvas preview or an available authorized browser view exists, inspect the actual saved rendering at overview and readable zoom. Refine overlaps or poor composition through another minimal position update. Use the browser only for visual inspection unless the user separately authorizes another editing method. If no rendering is available, explicitly report that coordinates were verified but appearance was not visually checked.

## Finish

Give the workflow link, the number of nodes moved, the main layout improvements, and verification results. Mention unchanged execution ordering only when checked. Distinguish a saved MCP update from a local proposal. Never claim a beautiful rendered result based only on successful tool status; report visual inspection limitations honestly.
