require 'rake/clean'
require 'rake/loaders/makefile'

CLEAN.include('*.o', '*.mf')
CLOBBER.include('*.exe')

source_files = Rake::FileList["*.c"]
object_files = source_files.ext(".o")
depend_files = source_files.ext(".mf") # New dependency file list.

task :default => "app.exe"

desc "Build the binary executable"
file "app.exe" => object_files do |task|
    sh "gcc #{object_files} -o #{task.name}"
end

rule '.o' => '.c' do |task|
    sh "gcc -c #{task.source}"
end

# The rule for creating dependency files.
rule '.mf' => '.c' do |task|
    sh "gcc -MM #{task.source} -MF #{task.name}"
end

# Explictly import each dependency file. If the file doesn't
# exist, the file task to create it is invoked.
depend_files.each do |dep|
    puts "importing #{dep}"
    import dep
end

# Declare an explict file task for each dependency file. This will
# use the rule defined to create .mf files defined earlier. This
# is necessary because it assures that the .mf file exists before
# importing.
depend_files.each do |dep|
  file dep
end