### git2go
---
https://github.com/libgit2/git2go

```go
// patch.go
package git

import "C"
import (
  "runtime"
  "unsafe"
)

type Patch struct {
  ptr *C.git_patch
}

func newPatchFromC(ptr *C.git_pathc) *Patch {
  if ptr == nil {
    return nil
  }
  
  patch := &Patch(
    ptr: ptr,
  )
  
  runtime.SetFinalizer(patch, (*Patch).Free)
  return patch
}





```

```
```

```
```


