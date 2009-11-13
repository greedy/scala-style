def cat_file(filename,to_file)
  File.open(filename) { |file| file.readlines.each { |line| to_file.puts(line) } }
end

INDEX="index.rst"
RST_FILE="README.rst"
NAME="scala_style_guide"

task :rst do
  File.open(RST_FILE,'w') do |out|
    cat_file(INDEX,out)
    `cd chapters ; ls ; cd -`.split(/\n/).each do |file|
      next if !(file =~ /\.rst$/)
      cat_file("chapters/" + file,out)
    end
  end
end

task :clean do
  `rm -f #{NAME}.tex`
  `rm -f #{NAME}.html`
end

task :default => :rst
task :latex => :rst do
  `rst2newlatex.py #{RST_FILE} > #{NAME}.tex`
end

task :html => :rst do
  `rst2html.py #{RST_FILE} > #{NAME}.html`
end
