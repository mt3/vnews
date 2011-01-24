require 'rake'
require 'rake/testtask'
require 'bundler'
Bundler::GemHelper.install_tasks

$LOAD_PATH.unshift File.join(File.dirname(__FILE__), 'lib')

desc "Save couchdb views in lib/couchviews.yml"
task :create_views do
  require 'couchrest'
  require 'yaml'
  require 'json'
  db = CouchRest.database! "http://localhost:5984/vnews"
  views = YAML::load File.read("lib/couchviews.yml")
  begin
    rev = db.get(views['_id'])['_rev']
    puts db.save_doc(views.merge('_rev' => rev))
  rescue RestClient::ResourceNotFound
    puts db.save_doc(views)
  end
end

desc "Run tests"
task :test do 
  $:.unshift File.expand_path("test")
  MiniTest::Unit.autorun
end

task :default => :test


