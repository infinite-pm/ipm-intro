# Meta / Implicit

Every ipmt node has an implicit SST kind (event, thing, or concept). These snippets make that implicit kind explicit by pointing the node at its SST meta-concept and then at `imp (sst)` - the umbrella concept for "an instance of an SST primitive."

```ipmt
Some event E1 ::e --> event (sst) ::c --> imp (sst) ::c
```
<!-- ipm-svg id=100 hash=db2bf8bf -->
![](../../_ipm/docs/examples/meta-ipm/100.ipm.svg)

```ipmt
Patrick --> thing (sst) ::c --> imp (sst) ::c
```
<!-- ipm-svg id=110 hash=e9a72a13 -->
![](../../_ipm/docs/examples/meta-ipm/110.ipm.svg)

```ipmt
human ::c --> concept (sst) ::c --> imp (sst) ::c
```
<!-- ipm-svg id=120 hash=1166c012 -->
![](../../_ipm/docs/examples/meta-ipm/120.ipm.svg)
