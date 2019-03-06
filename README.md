### afero
---
.go file
https://github.com/spf13/afero

```go
import "github.com/spf13/afero"

var AppFs = afero.NewMemMapFs()

var AppFs = afero.NewOsFs()

os.Open('/tmp/foo')
AppFs.Open('/tmp/foo')

Chmod(name string, mode os.FileMode) : error
Chtimes(name string, atime time.Time, mtime time.Time) : error
Create(name string) : File, error
Mkdir(name string, perm os.FileMode) : error
MkdirAll(path string, perm os.FileMode) : error
Name() : string
Open(name string) : File, error
OpenFile(name string, flag int, perm os.FileMode) : File, error
Remove(name string) : error
RemoveAll(name string) : error
Rename(oldname, newname string) : error
Stat(name string) : os.FileInfo, error


io.Closer
io.Reader
io.ReaderAt
io.Seeker
io.Writer
io.WriterAt

Name() : string
Readdir(count int) : []os.FileInfo, error
Readdirnames(n int) : []string, error
Stat() : os.FileInfo, error
Sync() : error
Truncate(size int64) : error
WriteString(s string) : ret int, err error


DirExists(path string) (bool, error)
Exists(path string) (bool, error)
FileContainsBytes(filename string, subslice []byte) (bool, error)
GetTempDir(subPath string) string
IsDir(path string) (bool, error)
IsEmpty(path string) (bool, error)
ReadDir(dirname string) (bool, error)
ReadFile(filename string) ([]byte, error)
SafeWriteReader(path string, r io.Reader) (err error)
TempDir(dir, prefix string) (name string, err error)
TempFile(dir, prefix string)(f File, err error)
Walk(root string, walkFn filepath.WalkFunc) error
WriteFile(filename string, data []byte, perm os.FileMode) error
WriteReader(path string, r io.Reader) (err error)


fs := new(afero.MemMapFs)
f, err := afero.Temp(fs, "", "ioutil-test")

fs := afero.NewMemMapFs()
afs := &afero.Afero{Fs: fs}
f, err := afs.TempFile("", "ioutil-test")


func TestExist(t *testing.T) {
  appFS := afero.NewMemMapFs()
  
  appFS.MkdirAll("src/a", 0755)
  afero.WriteFile(appFS, "src/a/b", []byte(), 0644)
  afero.WriteFile(appFS, "src/c", []byte("file c"), 0644)
  name := "src/c"
  _, err := appFS.Stat(name)
  if os.IsNotExist(err) {
    t.Errorf("file \"%s\" does not exist.\n", name)
  }
}


appfs := afero.NewOsFs()
appfs.MkdirAll("src/a", 0755)

mm := afero.NewMemMapFs()
mm.MkdirAll("src/a", 0755)

bq := afero.NewBasePathFs(afero.NewOsFs(), "/base/path")

fs := afero.NewReadOnlyFs(afero.NewOsFs())
_, err := fs.Create("/file.txt")

fs := afero.NewRegexpFs(afero.NewMemMapFs(), regexp.MustCopile(`\.txt$`))
_, err := fs.Create("/file.html")


httpFs := afero.NewHttpFs(<ExistingFS>)
fileserver := http.FileServer(httpFs.Dir(<PATH>))
http.Handle("/", fileserver)

base := afero.NewOsFs()
layer := afero.NewMemMapFs()
ufs := afero.NewCacheOnReadFs(base, layer, 100 * time.Second)

base := afero.NewOsFs()
roBase := afero.NewReadOnlyFs(base)
ufs := afero.NewCpyOnWriteFs(roBase, afero.NewMemMapFs())

fh, _ = ufs.Create("/home/test/file2.txt")
fh.WriteString("This is atest")
fh.Close()
```

```
go get github.com/spf13/afero
```

```
```


