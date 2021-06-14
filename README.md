suckless-101
============

Down the rabbit hole.

## Contributing

### Cloning

To contribute to suckless-101 project, first clone it locally

```sh
git clone https://github.com/sineemore/suckless-101.git
```

### Dependency

The project uses
[mdbook][mdbook-github]
to build the book from markdown files, you
can find installation instructions for mdbook on it's
[readme][mdbook-github-install]
.

You can find detail instruction on using mdbook in its
[user-guide][mdbook-user-guide]
.

### Project structure

The project files are organized as follows:

```
.
├── book                   // Build files
├── book.toml              // Meta-data
├── README.md              // You are here!
└── src                    // Source markdown files
    ├── <chapter>
    │    ├── intro.md      // Chapter introduction
    │    └── <section>.md  // Section contents
    └── SUMMARY.md         // Table of Contents
```

Things to keep in mind:

1. When contributing feel free to add yourself to the authors list in `book.toml`.
2. To create a new section or chapter, simply add an entry to `SUMMARY.md` and let mdbook create the required files for you.
You can refer to
[summary][mdbook-user-guide-summary]
section in mdbook's user guide for details.

### Building the book

#### Debugging

When editing the book you can get a live preview of the book using:

```sh
mdbook serve
```

This start a local http server that serves the book and automatically refreshes whenever changes are made to the book.

#### Production

The book site is build with:

```sh
mdbook build
```


<!-- Refrences --!>

[mdbook-github]: https://github.com/rust-lang/mdBook
[mdbook-github-install]: https://github.com/rust-lang/mdBook#installation
[mdbook-user-guide]: https://rust-lang.github.io/mdBook/
[mdbook-user-guide-summary]: https://rust-lang.github.io/mdBook/format/summary.html
