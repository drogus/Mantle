require 'bundler/setup'
require 'xcode_build'
require 'xcode_build/tasks/build_task'
require 'xcode_build/formatters/progress_formatter'

LIBRARY_VERSION = "1.4"
XCODEBUILD_LOG  = File.join(File.dirname(__FILE__), "xcodebuild.log")
GITHUB_USER     = 'henrikhodne'
GITHUB_REPO     = 'Mantle'

XcodeBuild::Tasks::BuildTask.new(:debug) do |t|
  t.scheme = "Mantle"
  t.configuration = "Debug"
  t.formatter = XcodeBuild::Formatters::ProgressFormatter.new
  t.xcodebuild_log_path = XCODEBUILD_LOG
end

namespace :test do
  XcodeBuild::Tasks::BuildTask.new do |t|
    t.project_name = 'Mantle.xcodeproj'
    t.scheme = "Mantle Mac"
    t.configuration = "Debug"
    t.sdk = "macosx10.8"
    t.formatter = XcodeBuild::Formatters::ProgressFormatter.new
    t.xcodebuild_log_path = XCODEBUILD_LOG
  end

  desc "Run unit tests"
  task :run => 'xcode:build' do
    sh "xcodebuild -scheme \"Mantle Mac\" -sdk $OSX_VERSION test"
  end
end

task :test => 'test:run'