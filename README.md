## To reproduce
 
 0. Setup x.clj and y.cljc (both deprecated via ns metadata), and z.clj requiring both
 1. Run `clj-kondo --cache true --lint src/x.clj src/z.clj src/y.cljc`
 
Ouput is:
```
src/z.clj:3:5: warning: Namespace x is deprecated.
linting took 11ms, errors: 0, warnings: 1
```
