# OCaml Resources

Another curated list of OCaml resources.

## License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">
  <img alt="Creative Commons License" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" />
</a>

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

---

## Static linking

The consensus seems to be something like this:

1. Use a Docker image with musl instead of glibc (e.g., Alpine Linux).
2. Add the proper flags to your Dune file (or directly to the OCaml compiler).
3. Compile your program inside that Docker container.

Blog posts

* [Creating Static Linux Binaries in OCaml](http://rgrinberg.com/posts/static-binaries-tutorial/)
  * Blog post by Rudi Grinberg
  * This the article that I used to get started statically linking OCaml programs.
* [Generating static and portable executables with OCaml](https://www.ocamlpro.com/2021/09/02/generating-static-and-portable-executables-with-ocaml/)
  * A newer article from OCamlPro.
  * Similar suggestions to the Grinberg post.
  * Also has info for MacOS.
* [How to Statically Link OCaml Programs](https://www.systutorials.com/how-to-statically-link-ocaml-programs/)

[OCaml Discuss](https://discuss.ocaml.org/) threads

* [Statically Link](https://discuss.ocaml.org/t/statically-link/1464)
* [Cross Platform (MacOSX/*nix) static linking](https://discuss.ocaml.org/t/cross-platform-macosx-nix-static-linking/2528)

GitHub issues

  * [Dune: How to create a statically linked library](https://github.com/ocaml/dune/issues/1904)
