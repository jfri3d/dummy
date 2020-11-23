## dummy
> Simple repo for testing Garden

## Steps

- set kubernetes context in `garden.env` (see `garden.env.template`)
```
CONTEXT=
```

- remove previous cached tests
```
$ kubectl delete -n garden-system $(kubectl get configmap -n garden-system -o name | grep test-result)
```

- run all tests
```
$ garden test
Running tests 🌡️

✔ providers                 → Preparing environment... → Done
   ✔ kubernetes                → Configuring... → Ready
✔ a                         → Getting build status for v-6242b56891... → Done (took 0 sec)
✔ b                         → Getting build status for v-abe48b9951... → Done (took 0 sec)
✔ a                         → Running int tests → Success (took 2.6 sec)
✔ a                         → Deploying version v-abe48b9951... → Done (took 4.3 sec)
   ℹ a                         → Resources ready
✔ b                         → Running int tests → Success (took 2.8 sec)

Done! ✔️
```

- ensure tests are cached
```
$ garden test
Running tests 🌡️

✔ providers                 → Getting status... → Cached
   ℹ Run with --force-refresh to force a refresh of provider statuses.
✔ b                         → int tests → Already passed
✔ a                         → int tests → Already passed

Done! ✔️
```

- 
