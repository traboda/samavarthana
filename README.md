## Install Instructions

### Set up Jekyll
The install instructions are tested _only_ on Ubuntu 22.04.

Install `ruby`:
```bash
sudo apt-get install ruby-full bundle
```

Specify a writable path for the `bundler` to download and extract `gem` packages required to run this project. For this, include the following lines in the `~/.zshrc` or `~/.bashrc` lines:
```bash
export BUNDLE_PATH=~/.gems
```

### Install Bundle Requirements

```bash
bundle install
```

### Serve Jekyll

```bash
bundle exec jekyll serve
```