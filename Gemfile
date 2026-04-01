# frozen_string_literal: true

source "https://rubygems.org"
spec.add_runtime_dependency "kramdown-parser-gfm"
gemspec

gem "jekyll", ENV["JEKYLL_VERSION"] if ENV["JEKYLL_VERSION"]
gem "kramdown-parser-gfm" if ENV["JEKYLL_VERSION"] == "~> 3.9"
