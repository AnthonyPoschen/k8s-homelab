.PHONY: all default
default: upgrade
all: upgrade

.PHONY: upgrade
upgrade: upgrade_flux upgrade_sealedsecrets

.PHONY: upgrade_flux
upgrade_flux:
	mkdir -p ./kustomization/base
	flux install --version=latest --namespace=flux-system --export >> ./kustomization/base/00-flux-system.yaml

.PHONY: upgrade_sealedsecrets
upgrade_sealedsecrets:
	$(eval VERSION := $(shell curl -sI https://github.com/bitnami-labs/sealed-secrets/releases/latest | grep "location: " | sed "s/.*\///"))
	curl -sL https://github.com/bitnami-labs/sealed-secrets/releases/download/${VERSION}/controller.yaml > sealed-secrets.yaml

# .PHONY: upgrade_linkerd
# upgrade_linkerd:
# 	linkerd install --crds --ignore-cluster > ./00-linkerd.yaml
# 	linkerd install --ignore-cluster --default-inbound-policy deny > ./10-linkerd.yaml
.PHONY: upgrade_istio
upgrade_istio:
	istioctl manifest generate -f ./istio-config.yaml > 10-istio-manifests.yaml
	istioctl manifest generate -f ./istio-config-local.yaml > 10-istio-manifests-local.yaml

