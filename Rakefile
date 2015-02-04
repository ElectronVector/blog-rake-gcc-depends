require 'rake/clean'

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