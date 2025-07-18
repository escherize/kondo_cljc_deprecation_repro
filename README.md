## To reproduce
 
 0. Setup x.clj and y.cljc (both deprecated via ns metadata), and z.clj requiring both
 1. Run `clj-kondo --cache true --lint src/x.clj src/z.clj src/y.cljc`
 
Ouput is:
```
src/z.clj:3:5: warning: Namespace x is deprecated.
linting took 11ms, errors: 0, warnings: 1
```

2. Check the cached values:

``` shell
$ cat .clj-kondo/.cache/v1/clj/x.transit.json | jet --from transit --to json | jq
{
  "x": {
    "row": 3,
    "col": 1,
    "fixed-arities": [
      0
    ],
    "name": "x",
    "ns": "x",
    "top-ns": "x",
    "type": "fn"
  },
  "deprecated": true,
  "filename": "src/x.clj"
}

$ cat .clj-kondo/.cache/v1/cljc/y.transit.json | jet --from transit --to json | jq
{
  "filename": "src/y.cljc",
  "clj": {
    "y": {
      "row": 3,
      "col": 1,
      "fixed-arities": [
        0
      ],
      "name": "y",
      "ns": "y",
      "top-ns": "y",
      "type": "fn"
    }
  },
  "cljs": {
    "y": {
      "row": 3,
      "col": 1,
      "fixed-arities": [
        0
      ],
      "name": "y",
      "ns": "y",
      "top-ns": "y",
      "type": "fn"
    }
  }
}
```


Notice that y.cljc isn't marked deprecated, (but should be)
