#
# Since the README is the style guide, here's what you need to know:
#
# - install docutils however you want
# - sudo gem install grancher
# - rake html # scala_style_guide.html contains the guide
#
# if your docutils commands are NOT like rst2html-2.6, do
# rake PY=<your extension>
#
# e.g.
#
# rake PY= html # runs rst2html
# rake PY=-2.5.py $ runs rst2html-2.5.py
#
# Not sure why the port maintainers did this insanity, but there you go
# You can also define this in your local environment and avoid the command line

require 'rake/clean'
require 'grancher/task'

RST_FILE="README.rst"
NAME="ScalaStyleGuide"
INDEX="#{NAME}.rst"

PY_DEFAULT="-2.6.py"
py = ENV['PY'] || PY_DEFAULT

CLEAN.include('*.aux')
CLEAN.include('*.log')
CLEAN.include('*.out')
CLEAN.include('*.tex')
CLEAN.include('*.dvi')
CLOBBER.include(NAME + '.html')
CLOBBER.include('index.html')
CLOBBER.include(NAME + '.pdf')

Grancher::Task.new do |g|
  g.branch = "gh-pages"
  g.push_to = "origin"
  g.file "index.html"
  g.file "styles.css"
  g.file "{NAME}.pdf"
end

def cat_file(filename,to_file)
  File.open(filename) { |file| file.readlines.each { |line| to_file.puts(line) } }
end

desc "Concatenate everything into README.rst"
task :rst do
  File.open(RST_FILE,'w') do |out|
    cat_file(INDEX,out)
    `cd chapters ; find . -name \\*.rst | sort ; cd -`.split(/\n/).each do |file|
      next if !(file =~ /\.rst$/)
      cat_file("chapters/" + file,out)
    end
  end
end

task :latex => :rst do
  `rst2newlatex#{py} #{RST_FILE} > #{NAME}.tex`
end

desc "Create PDF version"
task :pdf => :latex do
  `latex #{NAME}`
  `latex #{NAME}` # twice to get the TOC working...ah LaTeX
  `dvipdf #{NAME}`
end

desc "Pushes the current code to github pages"
task :ghpages => [:html,:pdf,:clean,:publish] do 
end

GH_HTML_ARGS = "--title='Scala Style Guide' --toc-entry-backlinks --toc-top-backlinks --link-stylesheet --stylesheet=styles.css"
task :html => :rst do
  `rst2html#{py} #{GH_HTML_ARGS} #{RST_FILE} > index.html`
end

task :default => [:html,:pdf]

