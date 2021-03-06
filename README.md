# OCaml Resources

A mishmash of OCaml resources and answers to some (un)common OCaml questions.

* [License](#license)
* [Docker & GitHub Actions](#docker--github-actions)
* [Dune](#dune)
* [Recursive modules](#recursive-modules)
  * [OCaml Discuss](#ocaml-discuss)
* [Row polymorphism](#row-polymorphism)
* [Static linking](#static-linking)
  * [Overview](#overview)
  * [Blog posts](#blog-posts)
  * [OCaml Discuss](#ocaml-discuss-1)
  * [GitHub issues](#github-issues)
* [Type declarations, interfaces, etc.](#type-declarations-interfaces-etc)

## License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">
  <img alt="Creative Commons License" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" />
</a>

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

---

## Docker & GitHub Actions

The "official" OCaml Docker images are the ones on [ocaml/opam](https://hub.docker.com/r/ocaml/opam) Dockerhub site.  A discussion about which images are official can be found [here](https://discuss.ocaml.org/t/which-ocaml-opam-docker-containers-to-use/8269).

* OCamlPro provides [slim Alpine OCaml images](https://gitlab.ocamlpro.com/OCamlPro/ocaml-docker-images).
  * You can use their [Dockerfile](https://gitlab.ocamlpro.com/OCamlPro/ocaml-docker-images/-/blob/master/Dockerfile) for an example of making a Docker image for OCaml development.
* An article about [caching Docker layers](https://evilmartians.com/chronicles/build-images-on-github-actions-with-docker-layer-caching#the-cache-dance-off)
  * Article is from a Ruby on Rails shop, but the Docker image caching works when building images for OCaml as well.

[OCaml Discuss](https://discuss.ocaml.org/) threads

* [Which OCaml Opam docker containers to use](https://discuss.ocaml.org/t/which-ocaml-opam-docker-containers-to-use/8269)

* [Lightweight OCaml Docker Images created by dune with Multi-Stage Builds](https://discuss.ocaml.org/t/lightweight-ocaml-docker-images-created-by-dune-with-multi-stage-builds/7958)
  * Inspired by [this article](https://medium.com/@bobbypriambodo/lightweight-ocaml-docker-images-with-multi-stage-builds-f7a060c7fce4).
* [Lightweight OCaml Docker Images with Multi-Stage Builds](https://discuss.ocaml.org/t/lightweight-ocaml-docker-images-with-multi-stage-builds/804)
  * Announcement post for [this article](https://medium.com/@bobbypriambodo/lightweight-ocaml-docker-images-with-multi-stage-builds-f7a060c7fce4)
  * Also discusses static linking [here](https://discuss.ocaml.org/t/lightweight-ocaml-docker-images-with-multi-stage-builds/804/3)

## Dune

* Disabling warnings in Dune: https://stackoverflow.com/a/57120928


## Recursive modules

### [OCaml Discuss](https://discuss.ocaml.org/) threads

* [How to deal with ???recursive??? modules?](https://discuss.ocaml.org/t/how-to-deal-with-recursive-modules/898)

## Row polymorphism

From a StackOverflow answer about [why OCaml records don't support row polymorphism](https://stackoverflow.com/a/15241144).

> The primary problem with using either structural subtyping or row polymorphism for all records is that it requires a significantly more involved runtime implementation, and consequently, also is more expensive. Where simple records can trivially be translated into plain tuples, with field access being just indexing, structural subtyping or row polymorphism require the ability to transparently "slice" an object, i.e. view it under a supertype with random fields removed. In general, this requires either field lookup by hashing (such as Ocaml's objects), or evidence passing techniques, where the index of every field used by a function or any of its callees has to be passed as a hidden argument in addition to the actual record (that's what SML# is doing, for example).

## Static linking

### Overview

The consensus seems to be something like this:

1. Use a Docker image with musl instead of glibc (e.g., Alpine Linux).
2. Add the proper flags to your Dune file (or directly to the OCaml compiler).
3. Compile your program inside that Docker container.

One thing to note.  You will see some blogs say you need `-ccopt -static`, or `-cclib -static-pie`.  There are a couple of variations.  But when compiling on Alpine 3.11, those will still give a dynamically linked exe according to `file` command.  According to `ldd` it is static, and it does work across linux OSes, however.

If you want it to be *static*, then you will need to also pass in `-no-pie`.  There is a lot written on `PIE` vs `no-PIE` binaries, and I encourage you to look at the security implications of `-no-pie`.  However, you will get a true static.

### Blog posts

* [Creating Static Linux Binaries in OCaml](http://rgrinberg.com/posts/static-binaries-tutorial/)
  * Blog post by Rudi Grinberg
  * This the article that I used to get started statically linking OCaml programs.
* [Generating static and portable executables with OCaml](https://www.ocamlpro.com/2021/09/02/generating-static-and-portable-executables-with-ocaml/)
  * A newer article from OCamlPro.
  * Similar suggestions to the Grinberg post.
  * Also has info for MacOS.
* [How to Statically Link OCaml Programs](https://www.systutorials.com/how-to-statically-link-ocaml-programs/)

### [OCaml Discuss](https://discuss.ocaml.org/) threads

* [Statically Link](https://discuss.ocaml.org/t/statically-link/1464)
* [Cross Platform (MacOSX/*nix) static linking](https://discuss.ocaml.org/t/cross-platform-macosx-nix-static-linking/2528)

### GitHub issues

  * [Dune: How to create a statically linked library](https://github.com/ocaml/dune/issues/1904)


## Type declarations, interfaces, etc.

* [Why do I need to repeat type declarations between interfaces and implementations (or how do I get around this)?](https://discuss.ocaml.org/t/why-do-i-need-to-repeat-type-declarations-between-interfaces-and-implementations-or-how-do-i-get-around-this/3350)
* [Avoiding duplicated definitions in module implementation and interface](https://discuss.ocaml.org/t/avoiding-duplicated-definitions-in-module-implementation-and-interface/1546)
  * Write types in `.mli` file and `include` where needed ([link](https://discuss.ocaml.org/t/avoiding-duplicated-definitions-in-module-implementation-and-interface/1546/3))
  * Public types in their own `.ml` file ([link](https://discuss.ocaml.org/t/avoiding-duplicated-definitions-in-module-implementation-and-interface/1546/4))

* [Simple top-down development in OCaml](https://blog.janestreet.com/simple-top-down-development-in-ocaml/)
  * Explains a trick to avoid code duplication when writing interface first and implementation later.

* Code duplication specifically with functors
  * [Functors in OCaml: triple code duplication necessary?](https://stackoverflow.com/questions/22348341/functors-in-ocaml-triple-code-duplication-necessary)
  * ["usual way to avoid writing out the module type twice is to define it in a separate ML file"]https://stackoverflow.com/a/22352773


* This SO question has a lot of suggestions: [Redundancy in OCaml type declaration (ml/mli)](https://stackoverflow.com/questions/3238509/redundancy-in-ocaml-type-declaration-ml-mli)
  * Have a module dedicated to type declarations and give it only an `.mli` ([link](https://stackoverflow.com/a/3268836))
  * Use some preprocessor or code generator tool ([link](https://stackoverflow.com/a/3238702))
  * Let `ocamlc` generate it for you: `ocamlc -i some.ml > some.mli` ([link](https://stackoverflow.com/a/3241147))
