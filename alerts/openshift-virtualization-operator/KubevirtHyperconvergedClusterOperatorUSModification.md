# KubevirtHyperconvergedClusterOperatorUSModification
<!-- Edited by apinnick, Nov 2022-->

## Meaning

This alert fires when a JSON Patch annotation is used to change an operand
of the HyperConverged Cluster Operator (HCO).

HCO configures OpenShift Virtualization and its supporting operators in
an opinionated way and overwrites its operands when there is an unexpected
change to them. Users must not modify the operands directly.

However, if a change is required and it is not supported by the HCO API,
you can force HCO to set a change in an operator by using JSON Patch annotations.
These changes are not reverted by HCO during its reconciliation process.

## Impact

Incorrect use of JSON Patch annotations might lead to unexpected results
or an unstable environment.

Upgrading a system with JSON Patch annotations is dangerous because the
structure of the component custom resources might change.

## Diagnosis

- Check the `annotation_name` in the alert details to identify the JSON
Patch annotation:

  ```text
  Labels
    alertname=KubevirtHyperconvergedClusterOperatorUSModification
    annotation_name=kubevirt.kubevirt.io/jsonpatch
    severity=info
  ```

## Mitigation

It is best to use the HCO API to change an operand. However, if the change
can only be done with a JSON Patch annotation, proceed with caution.

Remove JSON Patch annotations before upgrade to avoid potential issues.
