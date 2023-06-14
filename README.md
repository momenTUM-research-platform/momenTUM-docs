# momenTUM-docs: Documentation of the momenTUM Research Platform

The website for the documentation is: <br>

[MomunTUM Docs](https://docs.momentumresearch.eu/)

The banner url: <br>
![momenTUM banner](src/resources/images/banner.png)

## About
This repository contains the documentation of the momenTUM Research Platform. The documentation is written using [mdBook](https://rust-lang.github.io/mdBook/).

To run the mdBook locally, you must have `mdBook` installed. For installation instructions, see the [mdBook documentation](https://rust-lang.github.io/mdBook/). To open the mdBook locally, run:

```
mdbook serve --open
```

## Developers
The momenTUM Research Platform is developed at the [Technical University of Munich](https://www.tum.de/) in the [Professorship of Chronobiology & Health](https://www.sg.tum.de/en/chronobiology/home/) and at the [Max Planck Institute for Biological Cybernetics](https://www.kyb.tuebingen.mpg.de/en) under the supervision of Prof. Dr. Manuel Spitschan. The developer team consists of Constantin Goeldel, Blen Daniel Assefa and Marco Ma.


### Mermaid Installation and Update guide

1. Installing Mermaid
```
cargo install mdbook-mermaid
```
2. Then let ```mdbook-mermaid``` add the required files and configuration:
```
mdbook-mermaid install path/to/your/book
```
3. This will add the following configuration to your ```book.toml```:
```
[preprocessor.mermaid]
command = "mdbook-mermaid"

[output.html]
additional-js = ["mermaid.min.js", "mermaid-init.js"]
```
4. Run the command to launch your md-book
```
mdbook serve --open
```

