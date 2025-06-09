# made-funicular-postzegel
An overview of the umbrella of funicular postzegel. Or stamp in English.

## Interaction diagram
```mermaid
graph LR
  customer -->|REST| made-funicular-postzegel-backend-kotlin
  made-funicular-postzegel-reporter-kotlin -->|REST| made-funicular-postzegel-backend-kotlin
  subgraph distribution-center
  made-funicular-postzegel-reporter-client -->|Websocket| made-funicular-postzegel-reporter-kotlin
  made-funicular-postzegel-reporter-compose -->|Websocket| made-funicular-postzegel-reporter-kotlin
  made-funicular-postzegel-reporter-rs-gtk -->|Websocket| made-funicular-postzegel-reporter-kotlin
  mail-processor --> |Code-scanner| made-funicular-postzegel-reporter-kotlin
  end
  customer --> |Postage| mail-processor
```

## Deployments

```mermaid
graph TD
  made-duper-kubernetes --> kustomize
  kustomize --> made-funicular-postzegel-backend-kotlin
  made-funicular-postzegel-backend-kotlin --> postgres-backend
  postgres-backend --> persistent-volume
  kustomize --> made-funicular-postzegel-reporter-kotlin
  made-funicular-postzegel-reporter-kotlin --> postgres-reporter
  postgres-reporter --> persistent-volume
  made-funicular-postzegel-reporter-kotlin --> kafka-reporter
  kafka-reporter --> persistent-volume
  made-funicular-postzegel-reporter-kotlin --> service
  service --> made-funicular-postzegel-backend-kotlin
```

## Repos
- https://github.com/mvandermade/made-duper-kubernetes
- https://github.com/mvandermade/made-funicular-postzegel-reporter-kotlin
- https://github.com/mvandermade/made-funicular-postzegel-backend-kotlin
- https://github.com/mvandermade/made-funicular-postzegel-reporter-rs-gtk
- https://github.com/mvandermade/made-funicular-postzegel-reporter-compose
- https://github.com/mvandermade/made-funicular-postzegel-reporter-client
