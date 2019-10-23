

# Haskell 

### Development tools

Editor: VSCode 

- Plugins
  - [Haskell Syntax Highlighting](https://marketplace.visualstudio.com/items?itemName=justusadam.language-haskell)
  - [Hoogle search](https://marketplace.visualstudio.com/items?itemName=jcanero.hoogle-vscode)
  - [Haskell Language Server](https://marketplace.visualstudio.com/items?itemName=alanz.vscode-hie-server)
    - This one is the crown jewel but the setup is quite confusing 

### Stack

```brew install haskell-stack```

Set up a stack project:

```bash
stack new my-project
cd my-project
stack setup
stack build // or stack build --file-watch
stack exec my-project-exe
```

Run the app: 

```stack exec app```

(where ```app``` is defined in stack.yaml)

## Hakyll

Installation:
https://github.com/jaspervdj/hakyll/issues/684

## Resources

- [Cheatsheet](http://cheatsheet.codeslower.com/CheatSheet.pdf)
- [Explanation of Cabal and Stack](https://medium.com/@fommil/why-not-both-8adadb71a5ed)
- [Stanford lectures](http://www.scs.stanford.edu/11au-cs240h/notes/)
- [Continuous building](https://blog.ssanj.net/posts/2017-11-30-continuous-compilation-and-testing-through-stack-and-haskell.html)
- https://livebook.manning.com/book/get-programming-with-haskell/chapter-1/

