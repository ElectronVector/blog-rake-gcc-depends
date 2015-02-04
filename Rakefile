require 'rake/clean'

CLEAN.include('*.o')
CLOBBER.include('*.exe')

source_files = Rake::FileList["*.c"]
object_files = source_files.ext(".o")

task :default => "app.exe"

desc "Build the binary executable"
file "app.exe" => object_files do |task|
    sh "gcc #{object_files} -o #{task.name}"
end

rule '.o' => '.c' do |task|
    sh "gcc -c #{task.source}"
end