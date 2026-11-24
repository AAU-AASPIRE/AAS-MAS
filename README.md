<img src=".github/icon.png" alt="" width="96" align="right">

# AAS-MAS
The multi-agent orchestrator of the line: product, order and resource agents over XMPP (SPADE) that bid for process steps using the AASs' capabilities.

| Agent | What it does |
| --- | --- |
| Order agent | Takes an order (an `order` message over XMPP, or `POST /orders`) and starts a product agent per unit |
| Product agent | Follows its product's recipe: a call for proposals per step to the resource agents, chooses, has the product carried there (the shuttles bid too), accepts, waits for the result |
| Resource agent | One per module and shuttle, from its AAS: proposes for the capabilities it offers, and where a skill is missing plans one (modplan) and creates it online (modsync) before it runs the step |

The resource agents run a skill over the module's OPC UA server ([modlink](https://github.com/AAU-AASPIRE/modlink),
`--executor opcua`), through the AAS server and the DMP (`--executor dmp`), or simulated.

```powershell
python -m pip install -e ".[test]"
python -m lineagents --aas http://localhost:8081 --mqtt localhost:1883     # an agent per module, started on the AAS server's events
python -m pytest                                                            # with the aseptic line and the tools beside this repository
```

The XMPP server (Prosody) and the broker run in the lab stack ([deploy](https://github.com/AAU-AASPIRE/deploy), `aas/`).
The package is still called `lineagents`. Part of [AASPIRE](https://github.com/AAU-AASPIRE/aaspire).
