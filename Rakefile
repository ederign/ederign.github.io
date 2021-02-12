require 'jekyll'
require './_lib/wiki.rb'
require './_lib/wiki_processor.rb'

desc 'Build static content; Usage: `rake build`'
task :build do
  sh 'bundle exec jekyll build'
end

desc 'Start development server; Usage: `rake start`'
task :start do
  sh 'bundle exec jekyll serve --incremental'
end

desc 'Create new wiki; Usage: `rake "add_wiki[WIKI_NAME]"`'
task :add_wiki, [:wiki_name] do |t, args|
  wiki = Wiki.new(args.wiki_name)
  processor = WikiProcessor.new(wiki)
  processor.execute!
end
