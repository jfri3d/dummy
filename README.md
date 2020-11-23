## dummy
> Simple repo for testing Garden to identify when tests are not cached!

## Steps

### Test dependent on Container Service

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
✔ a                         → Getting build status for v-3494aa6c2f... → Done (took 0 sec)
✔ b                         → Getting build status for v-6556684743... → Done (took 0 sec)
✔ a                         → Deploying version v-3494aa6c2f... → Done (took 4.4 sec)
   ℹ a                         → Resources ready
✔ b                         → Running int tests → Success (took 3 sec)

Done! ✔️
```

- ensure tests are cached
```
$ garden test
Running tests 🌡️

✔ providers                 → Getting status... → Cached
   ℹ Run with --force-refresh to force a refresh of provider statuses.
✔ b                         → int tests → Already passed

Done! ✔️
```

- run tests with a "clean" clone
```
$ git clone https://github.com/jfri3d/dummy
$ garden test
Running tests 🌡️

✔ providers                 → Preparing environment... → Done
   ✔ kubernetes                → Configuring... → Ready
✔ b                         → int tests → Already passed

Done! ✔️
```

### Test dependent on Helm Service
