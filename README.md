# ecommerce-gitops

GitOps repository for the ecommerce sample application.

This repo is the handoff target for the app repo CI pipeline. The current
bootstrap phase keeps it focused on declarative config only:

- one initial environment
- service-level values files under `services/<service>/values.yaml`
- Argo CD-ready folder layout under `applications/` and `clusters/`
- no direct cluster sync yet

## Structure

- `services/` - service-specific Helm values updated by CI when images change
- `applications/` - future Argo CD Application or ApplicationSet manifests
- `clusters/` - environment-specific entry points and cluster overrides

## CI contract

The app repo updates `.image.tag` in each matching service values file on main
branch merges. Keep the following files present so handoff stays deterministic:

- `services/catalog/values.yaml`
- `services/cart/values.yaml`
- `services/checkout/values.yaml`
- `services/orders/values.yaml`
- `services/ui/values.yaml`

## Current phase

The repo is intentionally incomplete for Argo CD. It is prepared for GitOps
handoff first, then Argo CD bootstrap in a later step.
