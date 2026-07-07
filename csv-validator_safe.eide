#! CSV ingestion validator — untrusted a CSV row can only ever become one of a fixed set of decisions over a
#! closed type, never a tool argument. An injected instruction cannot be represented in the
#! closed type, so it is rejected at the trust boundary (and re-clamped at run time by extract).
#! @requires load — the csv ingestion validator sink
#! @effect io
#! @taint bridge — extract<Decision> turns the tainted input into a trusted decision
grant load

type Schema = Orders | Users | Events
type Decision = Ingest(Schema) | Reject

let raw = fetch<web>  # UNTRUSTED a CSV row — tainted
quarantined { let d = extract<Decision>(raw) }  # only a fixed Decision (payloads too) crosses
privileged { load(d) }  # act on the trusted decision only
