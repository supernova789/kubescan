# Kube-Scan Installation for a Kubernetes Cluster

Kube-Scan gives a risk score, from 0 (no risk) to 10 (high risk) for each workload. The risk is based on the runtime configuration of each workload (currently 20+ settings). The exact rules and scoring formula are part of the open-source framework KCCSS, the Kubernetes Common Configuration Scoring System.

Please notice that kube-scan currently scans the cluster when starting and will re-scan it every 24 hours. Thus, if you want to get an up-to-date risk score (e.g. after installing a new app), you should restart the kube-scan pod.

Please refer https://github.com/octarinesec/kube-scan for more details.

