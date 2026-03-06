# infra-fleet-ready

Repozytorium Fleet dla dwóch środowisk:
- `envs/dev` -> k3s
- `envs/prod` -> RKE2

## Jak używać
W Rancher Fleet utwórz osobne `GitRepo`:
- dla dev z `paths: ["envs/dev"]`
- dla prod z `paths: ["envs/prod"]`

Każdy katalog z `fleet.yaml` jest osobnym bundle.

## Kolejność logiczna
1. namespaces
2. storageclasses
3. minio-secret
4. minio
5. minio-bootstrap
6. cnpg-operator
7. database-core
8. database-pooler
9. database-backup
10. restore-test (opcjonalnie)

## Ważne uwagi
- Bundle Helm (`11-minio`) jest oddzielony od raw YAML/Kustomize.
- `12-minio-bootstrap` traktuj jako bundle jednorazowy. Po udanym bootstrapie możesz go wyłączyć albo usunąć z repo.
- Wstaw własne hasła i identyfikatory Rancher Project.
- Dla `envs/prod/05-storageclasses` zostawiłem przykład `longhorn-ha`. Jeżeli produkcja na RKE2 będzie miała inny CSI, podmień tylko storage class oraz odpowiednie patche DB/MinIO.
