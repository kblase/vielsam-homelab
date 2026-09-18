# vielsam-homelab
Das ist die IT Infrastruktur für das Wohnprojekt Vielsam


homelab/
├── bootstrap/
├── clusters/{dev,prod}/
├── platform/{argocd,cilium,cert-manager,...}/
└── applications/{grafana,...}/


                    Talos
                      │
                 Kubernetes
                      │
                    Cilium
                      │
                    Argo CD
                      │
          ┌───────────┴───────────┐
          │                       │
       Platform              Applications
          │                       │
     cert-manager             Grafana
     ingress                   Immich
     storage                   Jellyfin
     monitoring                ...

                  UPSTREAM
                     │
                     ▼
                 RENOVATE
                     │
                     ▼
                  Git PR
                     │
                     ▼
                ┌─────────┐
                │   DEV   │
                │ Argo CD │
                └────┬────┘
                     │
                  testing
                     │
                     ▼
              ┌─────────────┐
              │   STAGING   │
              │   Argo CD   │
              └──────┬──────┘
                     │
                  approval
                     │
                     ▼
              ┌─────────────┐
              │    PROD     │
              │   Argo CD   │
              └─────────────┘



                         Bitwarden
                             │
                             │ API
                             ▼
                    External Secrets
                         Operator
                             │
                             ▼
                    Kubernetes Secrets
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                        DEV Cluster                          │
│                                                             │
│  Talos → Kubernetes → Cilium → Argo CD → Platform → Apps   │
└─────────────────────────────────────────────────────────────┘
                             │
                       Promotion
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                       PROD Cluster                          │
│                                                             │
│  Talos → Kubernetes → Cilium → Argo CD → Platform → Apps   │
└─────────────────────────────────────────────────────────────┘