# Privileged Namespace Example

This example shows how to create a single namespace that has the ability to run privileged pods while other namspaces have a more restricted set of capabilties. This is done using PSPs. 

## Usage

1. Apply the two PSPs

```bash
kubectl apply -f psp-priv.yml
kubectl apply -f psp-restricted.yml
```

2. Apply the clusterroles

```bash
kubectl apply -f priv-cr.yml
kubectl apply -f restricted-cr.yml
```

3. Create the privileged namespace and the role binding for the default service account in that namespace

```bash
kubectl apply -f priv-ns-rb.yml
```

4. Apply the restricted cluster role binding to all other service accounts

```bash
kubectl apply -f restricted-ns-crb.yml
```

5. Now you can test applying the different deployment to each namespace. the `priv-deployment.yml` should only spin up pods when applying into the `privs` namespace.