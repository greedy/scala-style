INDEX="index.rst"
task :default do
  File.open("README.rst",'w') do |out|
    File.open(INDEX) { |index| index.readlines.each { |line| out.puts(line) } }
    `cd chapters ; ls ; cd -`.split(/\n/).each do |file|
      next if !(file =~ /\.rst$/)
      File.open("chapters/" + file) { |f| f.readlines.each { |line| out.puts(line) } }
    end
  end
end

task :clean do
  `rm README.rst`
end
