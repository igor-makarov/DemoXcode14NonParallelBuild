require 'censorius'

source 'https://cdn.cocoapods.org/'

use_frameworks!

# ignore all warnings from all pods
inhibit_all_warnings!

target 'DemoXcode14NonParallelBuild' do
  platform :ios, '15'

  #pod 'SwiftLint', '0.29.2'
end

post_install do |installer|
  generated_projects = installer.generated_projects
  generated_projects.each do |project|
    generator = Censorius::UUIDGenerator.new([project])
    generator.generate!
    generator.write_debug_paths unless ENV['CENSORIUS_SPEC_DEBUG'].nil?
  end
end

post_integrate do |_installer|
  user_project = Xcodeproj::Project.open('DemoXcode14NonParallelBuild.xcodeproj')
  user_project.sort
  generator = Censorius::UUIDGenerator.new([user_project])
  generator.generate!
  generator.write_debug_paths unless ENV['CENSORIUS_SPEC_DEBUG'].nil?
  user_project.save
end
