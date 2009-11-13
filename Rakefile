#$: << '../grancher/lib'
require 'grancher/task'

Grancher::Task.new do |g|
  g.branch = "gh-pages"
  g.push_to = "origin"
  g.file "index.html"

end

def cat_file(filename,to_file)
  File.open(filename) { |file| file.readlines.each { |line| to_file.puts(line) } }
end

INDEX="index.rst"
RST_FILE="README.rst"
NAME="scala_style_guide"


task :rst do
  File.open(RST_FILE,'w') do |out|
    cat_file(INDEX,out)
    `cd chapters ; find . -name \\*.rst | sort ; cd -`.split(/\n/).each do |file|
      next if !(file =~ /\.rst$/)
      cat_file("chapters/" + file,out)
    end
  end
end

task :clean do
  `rm -f #{NAME}.tex`
  `rm -f #{NAME}.html`
  `rm -f index.html`
end

task :default => :rst
task :latex => :rst do
  `rst2newlatex.py #{RST_FILE} > #{NAME}.tex`
end

task :html => :rst do
  `rst2html.py #{RST_FILE} > #{NAME}.html`
end

task :ghpages => [:rst,:index,:publish] do 
end

task :index do
  `rst2html.py #{RST_FILE} > index.html`
end
