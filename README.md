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

```hcl
module "control_plane" {
  source  = "app.terraform.io/example/proxmox-kube-compute/tofu" # or a pinned git ref
  version = "~> 0.1"

  cluster_name        = "example"
  control_plane_count  = 1
  # ...see variables.tf for the full input set
}

module "node_pool" {
  source = "./modules/node-pool" # relative to this module's checkout,
                                  # or the registry's nested-module address
  # ...
}
```

See `variables.tf`/`outputs.tf` in this repo's root (the control-plane module) and
under `modules/node-pool/` for the full input/output contract.
