## Rig custom provider example
This crate shows how you can implement your own custom provider for Rig in a local crate, by copying the `ollama` integrations and ensuring that it works when added from outside of `rig-core`.

## Differences
- We copied the `json_utils` file from the `rig-core` crate. Ideally you would just use Rust structs rather than fiddling with raw JSON, but this also works.
- Because of `impl TryFrom<rig::completion::Message> for Vec<Message>` causing orphan rule issues, Rig exposes a `ConvertMessage` trait which you can use instead.
  - Don't forget that you can also use free-standing functions if you'd like! There isn't really one way to go about this. Do what you want.
- We add the `worker` crate for WASM compatibility. You don't really have to do this if you don't want to, but it just won't be WASM compatible (and you'll need to remove the `worker::send` cfg macros).
