# Hermes → Sketch Lab diagram contract

> **Status: parked.** Excalidraw is Adam’s default editable diagram format. Use this contract only when Adam explicitly asks for Sketch Lab or when working on the Sketch Lab codebase.

Use this contract when Adam explicitly asks for a Sketch Lab visual explanation, system map, architecture sketch, or flow diagram. It is no longer the shared default for Ledger, Infrastructure, Programming, or Apple work.

## Default workflow

1. Confirm the diagram’s purpose and audience if it is unclear.
2. Make a concise `GeneratedGraph`:
   - normally 4–14 nodes;
   - never more than 48 nodes or 96 edges;
   - every node id is unique;
   - every edge references existing nodes and has no self-loop.
3. Use the local app origin: `http://127.0.0.1:5173/`.
4. Open `http://127.0.0.1:5173/?g=<URI-encoded graph JSON>`.
5. Briefly state the board name, the main layers or flow, and the number of nodes. Do not paste the full graph unless Adam asks.

The app accepts URI-encoded JSON directly in `?g=`, applies its own auto-layout, and lets Adam edit the result afterward.

## Graph shape

```json
{
  "name": "Diagram title",
  "layers": [{ "name": "Data", "color": "#38bdf8" }],
  "nodes": [
    {
      "id": "api",
      "label": "API",
      "kind": "icon",
      "icon": "microservice",
      "color": "#0f2740",
      "layer": 0
    }
  ],
  "edges": [
    { "from": "client", "to": "api", "label": "HTTPS", "directed": true }
  ]
}
```

- `kind`: `rect`, `circle`, `icon`, or `text`.
- Use `icon` for services, databases, cloud resources, users, clients, networks, queues, files, and infrastructure.
- Use `text` only for a standalone annotation.
- Use `#0f2740` for dark node fills by default. Layer accents should be bright, such as `#38bdf8`, `#4ade80`, `#fbbf24`, `#fb923c`, `#f472b6`, or `#c084fc`.
- Layers run bottom → top. Use 2–5 only when there is a real tiering; use `[]` and `layer: 0` for a flat diagram.
- Prefer directed edges for requests, data flow, dependencies, and sequences.

## Approved icon keys

`server`, `container`, `kubernetes`, `vm`, `function`, `microservice`, `router`, `switch`, `firewall`, `load-balancer`, `gateway`, `proxy`, `dns`, `cdn`, `network`, `vpn`, `database`, `cache`, `table`, `bucket`, `disk`, `archive`, `file`, `folder`, `queue`, `event-bus`, `stream`, `webhook`, `browser`, `desktop`, `laptop`, `phone`, `tablet`, `logs`, `dashboard`, `git`, `repo`, `pipeline`, `package`, `terminal`, `code`, `gear`, `rocket`, `bot`, `neural`, `search`, `lock`, `key`, `shield`, `vault`, `certificate`, `user`, `users`, `cloud`, `datacenter`, `location`, `sync`, `upload`, `download`, `workflow`, `decision`, `check`.

## Safety and quality

- Keep diagrams truthful: label assumptions and unknown boundaries rather than inventing systems or configuration.
- Do not put KRD/HR data, credentials, private keys, private network addresses, or sensitive internal architecture in generated or shared links.
- Do not use the browser’s direct OpenAI-key panel by default. Hermes creates the graph through the configured agent workflow, avoiding a second raw key and making the data boundary explicit.
- For a modification request, preserve useful node ids and existing structure unless Adam asks to replace it.
