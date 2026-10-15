# Goose on Tinfoil: bounded integration test

Public measured deployment configuration only. Application image and source are private.

One CPU-only, non-debug Tinfoil instance contains two roles: a Goose 1.54.0 runner with only internal networking, and an inference broker with an explicit Tinfoil/verification-host egress allowlist. The fixed task asks two specialists to compute synthetic revenue and data-quality results using GLM-5.3. The state-machine agent loop is enabled.

Only `/health`, authenticated `/run` and authenticated `/result` are exposed. One run is accepted per process lifetime. No arbitrary prompts, shell tools, file tools, uploads, persistent volumes, general web access, or production data are part of this test. Inference credentials are delivered at runtime over an attestation-verified connection, never committed to this repository or the image. Goose receives no real provider or provisioning credential.

Outbound vendor telemetry and OTel export are disabled for this test, not removed from Goose's code. This is not a hardened production agent product or a security certification. Stop the instance after the test; local scratch is ephemeral.

Private image: `ghcr.io/theforkproject-dev/goose-tinfoil-lab`, pinned by digest in `tinfoil-config.yml`.

Release workflows are taken from Tinfoil's public container template at `0eddc320b8f328d7a3c057152596934444ac2d75`. Runtime sources include Goose under Apache-2.0 and Tinfoil SDK under Apache-2.0; their required notices remain in the image.
