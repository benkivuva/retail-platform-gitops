# Incident Response Runbook

## 🚨 Alert: FlaskPodCrashLooping
**Severity:** Critical
**Description:** The Flask dashboard pods are restarting repeatedly and the app is likely down.

### Immediate Triage Steps:
1. **Check Pod Status:**
   `kubectl get pods -n flask`
2. **Check Pod Logs (look for Python Tracebacks or DB connection errors):**
   `kubectl logs -n flask deploy/flask-app --previous`
3. **Check if Database Secret exists:**
   `kubectl get externalsecret -n flask`
4. **Check ArgoCD Sync Status:**
   `kubectl get applications -n argocd flask`

### Common Causes:
*   **Database Connection Lost:** Cloud SQL instance is down or password changed. Check ESO sync status.
*   **Out of Memory (OOMKilled):** Check Grafana for memory spikes.
*   **Bad Image:** A bad CI build was deployed. Roll back by reverting the Git commit in the GitOps repo.
