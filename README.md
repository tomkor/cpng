# infra-fleet-noshared

Repo pod Rancher Fleet bez katalogu `shared/`.
Każdy bundle jest samowystarczalny i zawiera własne `base/`, `overlays/` albo własne pliki Helm values.

## Założenia
- `envs/dev` -> k3s
- `envs/prod` -> RKE2
- Helm tylko dla `11-minio`
- reszta jako raw YAML / Kustomize
- brak odwołań do plików poza katalogiem bundle
- `90-restore-test` traktuj jako opcjonalny bundle do ręcznego włączenia

## Co trzeba uzupełnić
- hasła w sekretach
- `field.cattle.io/projectId`
- manifesty:
  - `20-cnpg-operator/cnpg-operator.yaml`
  - `20-cnpg-operator/barman-plugin.yaml`

## Sugestia uruchomienia w Fleet
Dodaj dwa osobne GitRepo:
- dev -> path `envs/dev`
- prod -> path `envs/prod`


This variant is self-contained for Fleet/Kustomize: each overlays/current directory contains all resources it needs, without references to ../.. paths.
