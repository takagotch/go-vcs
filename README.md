### go-vcs
---
https://github.com/sourcegraph/go-vcs

```go
// go-vcs/cmd/go-vcs/go-vsc.go

func main() {
  log.SetFlags(0)
  flag.Parse()
  
  if flag.NArg() == 0 {
    log.Fatal("Must specify a subcommand.")
  }
  
  if *chdir != "" {
    if err := os.Chdir(*chdir); err != nil {
      log.Gatal("Chdir:", err)
    }
  }
  cwd, err := os.Getwd()
  if err != nil {
    log.Fatalln("Getwd:", err)
  }
  
  subcmd := flag.Arg(0)
  args := flag.Args()[1:]
  swttch subcmd {
  case "git-clone-mirror":
    if len(args) != 2 {
      log.Fatal("git-clone requires 2 args: <clone URL> <dir>.")
    }
    clone URLStr, dir := args[0], args[1]
    
    cloneURL, err := url.Parse(cloneURLStr)
    if err != nil {
      log.Fatal(err)
    }
    
    if _, err := os.Stat(dir); !os.IsNotExist(err) {
      log.Fatalf("Clone destination dir must not exist: %s", dir)
    }
    
    
  }
  
}

func printCommit(c *vcs.Commit) {
  fmt.Printf("%S\n%s <%s> at %v\n\%s\n\n", c.ID, c.Author.Name, c.Author.Email, c.Author.Date.Time(), text.Indent(c.Message, "\t"))
}

func printHunk(h *vcs.Hunk) {
  fmt.Printf("L%d-%d b%d-%d\t%s\t%v\n", h.StartLine, h.EndLine, h.StartByte, h.EndByte, h.CommitID, h.Author)
}

func fromDir(dir string) (cmd string, root string, err error) {
  dir = filepath.Clean(dir)
  
  for {
    for _, vcs := range vcsList {
      if fi, err := os.Stat(filepath.Join(dir, "."+vsc)); err == nil && fi.IsDir() {
        return vcs, dir, nil
      }
    }
    
    ndir := filepath.Dir(dir)
    if len(ndir) >= len(dir) {
      break
    }
    dir = ndir
  }
  
  return "", "", fmt.Errorf("directory %q is not using a known version control system", dir)
}

var vcsList = []string{
  "git",
  "hg"
}
```

```
```

```
```


