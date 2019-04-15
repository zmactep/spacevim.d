# SpaceVim Configuration

This is my SpaveVim configuration for a good life with Haskell, Rust, Python and Markdown.
To use this you'll need a small preparation of the system. The instruction is suitable for MacOS.

## Install

### Preparation for haskell

```bash
$ curl -sSL https://get.haskellstack.org/ | sh
$ stack setup
$ git clone git@github.com:haskell/haskell-ide-engine.git
$ cd haskell-ide-engine
$ vim shake.yaml # change resolver to a latest lts from stackage
$ vim stack-8.6.4.yaml # change resolver to a latest lts from stackage
$ stack install shake
$ stack ./install.hs hie-8.6.4
$ stack ./install.hs build-doc-8.6.4
```

### Preparation for Rust

```bash
$ curl https://sh.rustup.rs -sSf | sh
$ rustup update stable
$ rustup toolchain install stable
$ rustup component add rls-preview rust-analysis rust-src
```

### Preparation for Python

```bash
$ brew install python
$ pip3 install flake8 yapf autoflake isort ipython python-language-server
```

### Preparation for Markdown

```bash
$ brew install node
$ npm install -g remark
$ npm install -g remark-cli
$ npm install -g remark-stringify
```

### Preparation for a good life

One of the most annoying things in Vim for me is that the hotkeys do not work on russian keyboard layout. We can fix it with a plugin, that will change layout to basic US keyboard every time we will go to a Normal mode. It will also save the current layout before the switch to go back when you need it. The [plugin ](https://github.com/lyokha/vim-xkbswitch) itself is already bundled to this configuration. But we also need to install a [tool](https://github.com/vovkasm/input-source-switcher) to switch layouts from console.

I have prepared a Homebrew formula for that:
```ruby
class InputSourceSwitcher < Formula
  desc "Command line input source switcher for Mac."
  homepage "https://github.com/vovkasm/input-source-switcher"
  url "https://github.com/vovkasm/input-source-switcher/archive/v0.3.tar.gz"
  sha256 "c4bb51aae132e672c886ed8add7e31300be21569ec3e2867639e6ee23b38d049"
  depends_on "cmake" => :build

  def install
    system "cmake", ".", *std_cmake_args
    system "make", "install"
  end

  test do
    system "#{bin}/issw", "-l"
  end
end
```

We can install it using brew:
```bash
$ brew create https://github.com/vovkasm/input-source-switcher/archive/v0.3.tar.gz
$ # fix the formula like it is shown above
$ brew install input-source-switcher
```
