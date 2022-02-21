# frozen_string_literal: true

require 'html-proofer'
require 'rubocop/rake_task'
require 'jekyll'
require 'jsonlint/rake_task'

task default: %w[proof verify jsonlint rubocop]

task :build do
  config = Jekyll.configuration(
    'source' => './',
    'destination' => './_site'
  )
  site = Jekyll::Site.new(config)
  Jekyll::Commands::Build.build site, config
end

task proof: 'build' do
  HTMLProofer.check_directory(
    './_site', \
    assume_extension: true, \
    check_html: true, \
    disable_external: true
  ).run
end

JsonLint::RakeTask.new do |t|
  t.paths = %w[_site/data.json]
end

task :verify do
  ruby './verify.rb'
end

RuboCop::RakeTask.new
