# Go get tests

### 1. `go get github.com/Eclion/goget-test/sdk/v2`

```
go: downloading github.com/Eclion/goget-test/sdk/v2 v2.0.0-20250429155151-cb4aaa26e792
go: added github.com/Eclion/goget-test/sdk/v2 v2.0.0-20250429155151-cb4aaa26e792
```

=> OK but I'd prefer the dep in the go.mod without the date+hash

### 2. Tag `v2.0.0` then `go get github.com/Eclion/goget-test/sdk/v2@v2.0.0`

```
go: downloading github.com/Eclion/goget-test v2.0.0+incompatible
go: module github.com/Eclion/goget-test@v2.0.0 found (v2.0.0+incompatible), but does not contain package github.com/Eclion/goget-test/sdk/v2
```

=> NOK

### 3. Branch `v2.0.1` then `go get github.com/Eclion/goget-test/sdk/v2@v2.0.1`

```
go: github.com/Eclion/goget-test/sdk/v2@v2.0.1: invalid version: unknown revision sdk/v2.0.1
```

=> NOK

### 4. Branch `sdk/v2.0.2` then `go get github.com/Eclion/goget-test/sdk/v2@v2.0.2`

```
go: github.com/Eclion/goget-test/sdk/v2@v2.0.2: invalid version: resolves to version v2.0.0-20250429155151-cb4aaa26e792 (v2.0.2 is not a tag)
```

=> NOK: not added in go.mod

### 5. Tag `sdk/v2.0.3` then `go get github.com/Eclion/goget-test/sdk/v2@v2.0.3`

```
go: downloading github.com/Eclion/goget-test/sdk/v2 v2.0.3
go: upgraded github.com/Eclion/goget-test/sdk/v2 v2.0.0-20250429155151-cb4aaa26e792 => v2.0.3
```

```
# go.mod

module github.com/Eclion/goget-test

go 1.24.0

require github.com/Eclion/goget-test/sdk/v2 v2.0.3 // indirect
```

=> Meh: the entry in go.mod is correct, but the tag is not semver anymore, and I don't know any better.
