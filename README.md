# terraform-proxmox-kube-compute

This repository is a **generated, read-only release mirror**. It contains the
Proxmox-provider slice of [kube-compute](https://github.com/bbaliyan/kube-compute),
published here on every `kube-compute` release that changes Proxmox-related code.

**Do not open issues or pull requests against this repo** — it is a build artifact,
not a place where development happens. Issues and PRs are disabled here for exactly
this reason. File bugs, feature requests, and changes against
[kube-compute](https://github.com/bbaliyan/kube-compute) instead.

This repo's commit history is a simple, append-only sequence of one commit per
release (`release: vX.Y.Z`) — it is never rewritten or force-pushed, so a local
clone never diverges from `origin`.

## License

Apache-2.0 — see `LICENSE`/`NOTICE`. Same license as `kube-compute`.

## Usage

Both options below resolve to *this* repo only — never to the private
`kube-compute` monorepo, which isn't publicly consumable. The registry address's
middle segment (`kube-compute`) is just this repo's *name* component under
OpenTofu's `terraform-<target>-<name>` naming convention, not a reference to
that other repo.

```hcl
module "control_plane" {
  # Option 1: OpenTofu Registry (once published) — resolves to this repo's
  # root module. No hostname prefix needed for the public registry.
  source  = "bbaliyan/kube-compute/proxmox"
  version = "~> 0.1"

  # Option 2: pin a git ref against this repo directly instead:
  #   source = "github.com/bbaliyan/terraform-proxmox-kube-compute?ref=<tag>"

  cluster_name        = "example"
  control_plane_count = 1
  # ...see variables.tf for the full input set
}

module "node_pool" {
  # Nested submodules use the registry's // convention, same version constraint
  # as the root module above — still this repo's modules/node-pool/:
  source  = "bbaliyan/kube-compute/proxmox//modules/node-pool"
  version = "~> 0.1"
  # ...see modules/node-pool/variables.tf for the full input set
}
```

See `variables.tf`/`outputs.tf` in this repo's root (the control-plane module) and
under `modules/node-pool/` for the full input/output contract.
