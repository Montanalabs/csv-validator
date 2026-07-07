#! VULNERABLE csv-validator — feeds the untrusted input straight to the tool, no extraction.
#! check -> UNSAFE: tainted data cannot reach a capability.
grant load

let raw = fetch<web>
privileged { load(raw) }  # tainted -> tool: REJECTED
