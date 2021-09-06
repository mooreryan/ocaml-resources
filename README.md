# OCaml Resources

Another curated list of OCaml resources.

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
