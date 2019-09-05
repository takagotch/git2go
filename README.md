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









func (v *Repository) PatchFromBuffers(oldPath, newPath string, oldBuf, newBuf []byte, opts *DiffOptions) (*Patch, error) {
  var patchPtr *C.git_patch
  
  oldPtr := toPointer(oldBuf)
  newPtr := toPointer(newBuf)
  
  cOldPath := C.CString(oldPath)
  defer c.free(unsafe.Pointer(cOldPath))
  
  cNewPath := C.CString(newPath)
  defer C.free(unsafe.Pointer(cNewPath))
  
  copts, _ := diffOptionsToC(opts)
  defer freeDiffOptions(copts)
  
  runtime.LockOSThread()
  defer runtime.UnlockOSThread()
  
  ecode := C.git_patch_from_buffers(&patchPtr, oldPtr, C.size_t(len(oldBuf)), cOldPath, newPtr, C.size_t(len(newBuf)), cNewPath, copts)
  runtime.KeepAlive(oldBuf)
  runtime.KeepAlive(newBuf)
  if ecode < 0 {
    return nil, MakeGitError(ecode)
  }
  return newPathFromc(patchPtr), nil
}
```

```
```

```
```


