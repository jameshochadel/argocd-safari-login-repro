# To reproduce:

```
kustomize build | kubectl apply -f -

# wait for pods to be running.
# once available, copy name of argocd-server-* pod, which is the default admin password.
watch kubectl get pods -n argocd-repro

# probably in a tmux pane...
kubectl port-forward -n argocd-repro svc/argocd-server 8080:443

# additionally...
kubectl logs 
```

Then:

* Open Safari and navigate to `localhost:8080`.
* Attempt to login with username = `admin` and password = the `argocd-server` pod name.

Expected: I am logged in. 
Actual: I am redirected to the same login page, which does not indicate any error.

Finally:

* Open Chrome and navigate to `localhost:8080`
* Attempt to login with the same username and password.
* Observe: The login succeeds as expected.

# More Info

For logs from the argocd-server pod, see `logs.txt`.
For network requests as recorded in the Safari Web Inspector, see `network-requests.txt`.
For a screenshot of the request timeline, see `safari-timeline.png`.
